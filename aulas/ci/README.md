# Integração contínua

## O que é
- É o processo de integrar modificações do codebase de forma contínua e automatizada, evitando assim erros humanos de verificação, garantindo mais agilidade e segurança no processo de desenvolvimento de software.

## Principais processos

- Execução de testes
- Linter
- Verificação de qualidade de código
- Verificações de segurança
- Geração de artefatos prontos para o processo de deploy
- Identificação da próxima versão a ser gerada no software
- Geração de tags e releases

## Github Actions 
![](https://github.com/PedroGuilhermeSilv/full-cycle/blob/develop/aulas/ci/img/githubactions.png)

1. Crie uma pasta chamada de .github/main/arquivo.yaml. 
2. Dentro do arquivo.yaml estará as instruções dos testes que deeseja realizar.
- A [documentação](https://docs.github.com/pt/actions) do github possui vários exemplos de uso. 

## Status check
- Você pode incluir uma lista de testes para eventos específicos em seu repositório Git. 
1. Adicione no arquivo.yaml
2. No repositório do github vá em settings->branchs.
3. Adicione a opção "Require status check"

- Podemos também trabalhar com multi versões usando [Strategy Matrix](https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs), dessa forma podemos rodar os testes em diferentes versões como: go 1.14, go 1.15 e etc...

## Buildando uma imagem docker

- É possível também subir uma imagem docker para realizar os testes de nosso dockerfile. [Saiba Mais](https://github.com/marketplace/actions/build-and-push-docker-images)

## Sonarqube
- É umma ferramenta open source que faz a análise de código para varificar a qualidade e integridade.
- Rules: serão as regras de determinada linguagens de progrmação.
- Quality Profiles: serão perfis que contém as regras para serem atribuidos a determinado projeto.
- Quality Gates: verifica se o projeto está passando ou não.