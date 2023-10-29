# Full Cycle

# Docker
1 - Containers:
- Containers são na verdade processos isolados que simulam um sistema operacional.
- CGroups permitu separa recursos(memória, trehads) para determinado processo.
- OFS (Overlay File System), para cada nova imagem criada não se repete dependências já instaladas mas sim as que foram alteradas.

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