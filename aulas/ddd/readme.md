# DDD - Domain Driven Design

## Como DDD pode ajudar ?

- Entender com profundidade o domínio e subdomínios da aplicação.
- Ter uma linguagem universal entre todos os envolvidos. 
- Criar o design estratégico utilizando Bounded Contexts.
- Criar o design tático para conseguirm mapear e agregar as entidades e objetos de valor da aplicação, bem como os eventos de domínio.
- Clareza do que é complexidade de negócio e complexidade técnica.

## Domínio e Subdomínio
- Core Domain
- Support Domain
- Generic subdomain (software auxiliares)

## Problema vs Solução
- Problema: Visão geral do domínio e suas complexidades (subdomíno->contexto)
- Solução: Análise e modelagem do domínio. 

## Bounded Contexts
- Delimitação de um contexto onde todos possam usar uma linguagem universal.
- Quando se começa a utilizar diferentes linguagens em um contexto é um indicio que devemos separar em diferentes áreas de aplicação.

## Elementos Transversais 
- Imagine que uma entidade `cliente` é a mesma para diferente contextos e ne outro cenário o `ticket` tem o mesmo nome mas tem signficado diferente entre dois contextos. Ambas situações devemos tratar as entidade de maneira independente entre si, isso ajudará com que um contexto não dependa de outro e crie um monstro.

## Context Mapping

![Context Mapping](https://github.com/PedroGuilhermeSilv/full-cycle/blob/develop/aulas/ddd/img/context_mapping.png )

- Shared: compartilhamento entre contextos.
- Upstream: fornecedor de dados.
- Downstream: recepitor dos dados.
- ACL(anti corruption layer): faz o intermédio entre o contexto e um programa externo para minimizar a dependência. 

### Documentation
https://github.com/ddd-crew/context-mapping

## Entite
- Uma entidade deve ser única e de fácil distinção independente de seus atributos.
- Regras de negócio: A entidade deve incorporar as regras de negócio da aplicação. Não é suficiente apenas ter getters e setters; isso resultaria em uma entidade anêmica. Devemos, por exemplo, utilizar métodos como "changeName" em vez de simplesmente "setName".
- Consistência: Uma entidade sempre deve ter o mínimo para cumprir uma regra de negócio, por exemplo, um custumer sem nome é algo que provavelmente deve infrigir a regra de negócio da aplicação. 