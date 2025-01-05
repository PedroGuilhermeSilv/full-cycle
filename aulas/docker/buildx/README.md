## Resumo do capítulo

## 1. Introdução ao Docker Buildx

###  O Docker Buildx é uma ferramenta avançada que estende o comando docker build com funcionalidades poderosas, permitindo:

- Builds Multiplataforma: Construa imagens para várias arquiteturas (e.g., amd64, arm64) a partir de uma única máquina.
- Ambiente Isolado: Use um ambiente de build separado, evitando conflitos com o Docker daemon principal.
- Emulação com qemu: Permite construir imagens para arquiteturas diferentes da do host.
- Gerenciamento Avançado de Cache: Reutilize camadas de build para acelerar o processo.
- Docker-in-Docker: Executa builds dentro de um container com seu próprio Docker daemon.

## 2. Conceitos Fundamentais
### Builders e Contextos

- Builder: Um ambiente onde os builds são executados. Pode ser local ou remoto e possui configurações específicas.
- Contexto: Define qual Docker daemon o Docker CLI usará. Pode apontar para um daemon local ou remoto.

Nota: Um builder pode estar associado a um contexto, e isso afeta como ele é gerenciado.
### Drivers: docker vs docker-container
### Driver docker

- Usa o Docker daemon local.
- Builds são executados diretamente no daemon principal.
- Suporte limitado para builds multiplataforma sem emulação.
- Não cria um ambiente isolado.

### Driver docker-container

- Cria um container separado que executa um Docker daemon interno (Docker-in-Docker).
- Suporta builds multiplataforma completos usando qemu para emulação.
- Oferece um ambiente de build isolado, evitando interferências com o daemon principal.
- Permite configurações avançadas de cache e builds distribuídos.

### Ambiente Isolado e Docker-in-Docker

Quando você usa o driver docker-container, o Buildx cria um container que roda um daemon Docker interno. Isso significa:

- O build ocorre em um ambiente separado, não afetando o Docker daemon principal.
- O container tem seu próprio cache, configurações e pode usar qemu para emulação.
- É essencialmente um "Docker-in-Docker", onde um Docker daemon está rodando dentro de um container Docker.

### O que é qemu e por que é importante?

QEMU: Quick Emulator, uma ferramenta de emulação que permite executar programas compilados para uma arquitetura em outra diferente.
No contexto do Docker Buildx, qemu permite construir imagens para arquiteturas diferentes da do host (e.g., construir uma imagem amd64 em um host arm64).
O Buildx com driver docker-container configura automaticamente o qemu dentro do ambiente isolado, facilitando os builds multiplataforma.

## 3. Criando e Gerenciando Builders
### Criando um Builder com docker-container

Para criar um novo builder usando o driver docker-container:

```bash
docker buildx create --name meu-builder --driver docker-container --use
```
- name: Nome do builder.
- driver docker-container: Especifica o driver.
- use: Define o builder como o ativo.

#### Inicializando o Builder com -bootstrap

Após criar o builder, inicialize-o:
```bash
docker buildx inspect --bootstrap
```

- O -bootstrap configura o ambiente, incluindo a configuração do qemu para emulação.
-  Se o builder não estiver ativo, ele será inicializado, e o container correspondente será criado.

### Listando e Selecionando Builders

Listar builders:
```bash
docker buildx ls
```

Exibe todos os builders, seus drivers, contextos e status.

### Selecionar um builder existente:
```bash
docker buildx use meu-builder
```

Define o builder especificado como o ativo.

### Removendo Builders e Contextos

Remover um builder:
```bash
docker buildx rm meu-builder
```

- Se o builder estiver associado a um contexto:

- Se você receber um erro semelhante a:

      failed to remove desktop-linux: context builder cannot be removed, run `docker context rm desktop-linux` to remove this context

    Isso significa que desktop-linux é um contexto, não apenas um builder. Nesse caso, remova o contexto:
```bash
docker context rm desktop-linux
```

Depois, remova o builder se necessário.

Nota: Um builder associado a um contexto não pode ser removido até que o contexto seja removido.
##  4. Executando Builds Multiplataforma
Usando qemu para Emulação de Arquitetura

- qemu permite que você construa imagens para arquiteturas diferentes da do host.
- O Buildx com docker-container configura o qemu automaticamente dentro do ambiente isolado.
- Isso é essencial para builds multiplataforma confiáveis.

###  Builds Multiplataforma com docker-container

Exemplo: Construir uma imagem para amd64 em um host arm64 (e vice-versa).

- Crie e inicialize o builder (como mostrado anteriormente).
- Execute o build multiplataforma:
```bash
docker buildx build --platform linux/amd64,linux/arm64 -t meu-repositorio/minha-imagem:latest --push .
```

- **`-platform`**: Especifica as arquiteturas alvo.
- **`-push`**: Necessário para builds multiplataforma, pois a imagem resultante precisa ser enviada a um registry.

### Comparação com o Driver docker

    Driver docker:
        Usa o Docker daemon local.
        Não suporta emulação com qemu por padrão.
        Builds multiplataforma são limitados à arquitetura do host.
    Limitações:
        Em um host arm64, você não conseguirá construir imagens amd64 corretamente sem qemu.
        O driver docker não configura qemu automaticamente.

## 5. Gerenciamento de Cache no Buildx

O Buildx oferece opções avançadas de cache para acelerar seus builds.
Cache Local

Para usar cache local:
```bash
docker buildx build --cache-to type=local,dest=./cache --cache-from type=local,src=./cache -t minha-imagem .
```

- cache-to: Define onde o cache será salvo.
- cache-from: Especifica de onde carregar o cache existente.

### Cache Remoto em Registries

Para armazenar o cache em um registry remoto (como o Docker Hub):
```bash
docker buildx build \
  --cache-to type=registry,ref=meu-repositorio/minha-imagem:cache,mode=max \
  --cache-from type=registry,ref=meu-repositorio/minha-imagem:cache \
  -t minha-imagem .
```

Isso permite compartilhar o cache entre diferentes ambientes e máquinas.

### Limpeza de Cache com buildx prune

Para liberar espaço em disco removendo caches antigos:

    Remover todo o cache:
```bash
docker buildx prune -a
```

### Remover cache não utilizado nas últimas 24 horas:
```bash
docker buildx prune --filter=until=24h
```

## 6. Exemplos Práticos Passo a Passo
- Exemplo 1: Criando e Usando um Builder

Criar um builder com docker-container:
```bash
docker buildx create --name meu-builder --driver docker-container --use
```

Inicializar o builder:
```bash
docker buildx inspect --bootstrap
```

Verificar se o builder está ativo:
```bash
docker buildx ls
```

- Exemplo 2: Build Multiplataforma de uma Aplicação Go

Usando o Dockerfile da aplicação Go fornecida:
Dockerfile:
```dockerfile

FROM golang:latest AS builder

LABEL maintainer="Wesley Willians"

WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 go build -ldflags="-s -w" -o server main.go

# Final stage
FROM scratch
USER 1001
COPY --from=builder /app/server /server
ENTRYPOINT ["./server"]
```

Passos:

- Criar e inicializar o builder (se ainda não o fez).
- Executar o build multiplataforma:
```bash
docker buildx build --platform linux/amd64,linux/arm64 -t meu-repositorio/minha-aplicacao-go:latest --push .
```

Verificar a imagem no registry: As imagens para ambas as arquiteturas estarão disponíveis.

### Exemplo 3: Gerenciamento de Builders e Contextos

    Listar builders e contextos:
```bash
docker buildx ls
docker context ls
```

Remover um builder associado a um contexto: Primeiro, remover o contexto:
```bash
docker context rm meu-contexto
```

Depois, remover o builder:
```
docker buildx rm meu-builder
```
