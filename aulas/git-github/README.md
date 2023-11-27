# Padrões e técnicas avançadas com Git e Github
## Padrões de branch
![](https://github.com/PedroGuilhermeSilv/full-cycle/blob/main/aulas/git-github/img/gitflow.png)

1. Branches Principais:
    - main: Representa a linha principal de desenvolvimento e contém apenas código estável e testado.
    - develop: É o ramo de integração, onde as contribuições individuais são mescladas antes de serem lançadas.
    > git checkout develop

2. Branches de Feature (Funcionalidade):
    - feature/{nome-da-feature}: Criados a partir do ramo develop para desenvolver novas funcionalidades. Após a conclusão, são mesclados de volta para develop.
    > git checkout -b feature/{nome-da-feature}
    > git checkout develop
    > git merge feature/{nome-da-feature}
    > git branch -d feature/{nome-da-feature}


3. Branches de Release (Versão):
    - release/{versão}: Ramo criado a partir de develop quando há recursos suficientes para uma versão. É usado para correções finais e preparação para lançamento. Após testes, é mesclado em master e develop, e uma tag é criada.
                
4. Branches de Hotfix (Correção Rápida):
    - hotfix/{nome-da-correcao}: Criados a partir de master para corrigir problemas críticos em produção. Assim que a correção é feita, é mesclada em master e develop, e uma tag é criada.

## Repositório Git-Flow
Foi criado um repositório para implementar a metodoogia git-flow [Gii-flow](https://github.com/PedroGuilhermeSilv/git-flow).