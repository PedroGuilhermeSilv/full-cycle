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

- Crie uma pasta chamada de .github/main/arquivo.yaml. Dentro do arquivo.yaml estará as instruções dos testes que deeseja realizar, na [documentação](https://docs.github.com/pt/actions) do github temos vários exemplos de uso. 

## Status check
Você pode incluir uma lista de testes para eventos específicos em seu repositório Git, como, por exemplo, exigir a execução de testes antes de mesclar um pull request ou quando realizar um push..