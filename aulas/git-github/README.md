# Padrões e técnicas avançadas com Git e Github
## Padrões de branch
![](https://github.com/PedroGuilhermeSilv/full-cycle/blob/main/aulas/docker/img/docker-funciona.png)

1. Branches Principais:
    - master: Representa a linha principal de desenvolvimento e contém apenas código estável e testado.
    - develop: É o ramo de integração, onde as contribuições individuais são mescladas antes de serem lançadas.

- Branches de Feature (Funcionalidade):

    feature/{nome-da-feature}: Criados a partir do ramo develop para desenvolver novas funcionalidades. Após a conclusão, são mesclados de volta para develop.

- Branches de Release (Versão):

    release/{versão}: Ramo criado a partir de develop quando há recursos suficientes para uma versão. É usado para correções finais e preparação para lançamento. Após testes, é mesclado em master e develop, e uma tag é criada.

- Branches de Hotfix (Correção Rápida):

    hotfix/{nome-da-correcao}: Criados a partir de master para corrigir problemas críticos em produção. Assim que a correção é feita, é mesclada em master e develop, e uma tag é criada.