# Full Cycle

# Docker
1 - Containers:
- Containers são na verdade processos isolados que simulam um sistema operacional.
- CGroups permitu separa recursos(memória, trehads) para determinado processo.
- OFS (Overlay File System), para cada nova imagem criada não se repete dependências já instaladas mas sim as que foram alteradas.
- Containers são imutáveis, não faça alterações nos arquivos dos containers pois após você matar o processos as mudanças seram perdidas.

2 - Imagens:
- São camadas de dependências e essas mesmas dependências podem ser usadas em outras imagens.

3 - Dockerfile:
- Arquivo declarativo para construir imagens
FROM: ImgaemName
RUN: Comandos
EXPOSE: 8000

4 - Volumes, Network
- Os volumes fazem o docker compartilhar uma pasta local junto a imagem docker para que os arquivos não sejam perdidos.
- O Network permite que as imagens possas se comunicar dentro do docker.

![](https://github.com/PedroGuilhermeSilv/full-cycle/blob/main/Aulas/Docker/img/docker-funciona.png)

5 - Comandos:
Mostra os containers que estão rodando.
```bash
$ docker ps
```
Mostra os containers que estão rodando e os que já executaram mas foram abortados.
```bash
$ docker ps -a
```
"-i" significa interativo, fazendo com que seu terminal fique ligado diretamente no container.
"-t" signfica TTY, possibilita digitar comandos no terminal.
```bash
$ docker run -it ubuntu bash
```
"--rm" após encerrar o container ele apagará seu histórico.
```bash
$ docker run -it --rm ubuntu bash
```

"-p" passa a porta local (8080) que apontará a porta do conatiner (80)
```bash
$ docker run -p 8080:80 nginx
```

"-d" desacopla o terminal do container e "--name" passa o nome do container
```bash
$ docker run --name ngnix -d -p 8080:80 nginx
```

"start" inicia o container 
```bash
$ docker start nome_container
```

"rm" remove p container e "-f" força a remoção
```bash
$ docker rm nome_container -f
```
o "exec" executa comando dentro do container. No exemmplo abaixo ele irá retornar os arquivos que estao no container.
```bash
$ docker exec nome_container ls
```
Já no exemplo abaixo ficamos dentro do container com o bash ativo.
```bash
$ docker exec -it nome_container bash
```


 Aula
 [] #F0017
 