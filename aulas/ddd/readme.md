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

## Entite:
- Uma entidade deve ser única e de fácil distinção independente de seus atributos.
- A entidaded sempre deve representar o estado atual e correto.
- Consistência: Uma entidade sempre deve ter o mínimo para cumprir uma regra de negócio, por exemplo, um custumer sem nome é algo que provavelmente deve infrigir a regra de negócio da aplicação. 

## Regra de Negócio:
- Regras de negócio: A entidade deve incorporar as regras de negócio da aplicação. Não é suficiente apenas ter getters e setters; isso resultaria em uma entidade anêmica. Devemos, por exemplo, utilizar métodos como "changeName" em vez de simplesmente "setName". Toda atividade que envolva mexer com nossa entitade pode se tornar uma regra de negócio.

## Principio da autovalidação:
- Uma entidade deve se autovalidar, ou seja, não deve depender de serviços externos para garantir a integridade dos seus dados.

## Entidade vs ORM
- A entidade é a regra de negócio da empresa o ORM é a tabela no banco de dados.
- São dois pilares diferentes da aplicação.
Ex:
- Entity
    - custumer.ts(regra de negócio)
- Infra
    - Model
        - custumer.ts(get,set)

## Value Objects
- Imutabilidade: Os objetos de valor são geralmente imutáveis, o que significa que uma vez criados, seus estados não podem ser alterados. Isso ajuda a garantir a consistência e a previsibilidade em um sistema.

- Sem identidade própria: Ao contrário das entidades, os objetos de valor não têm uma identidade única. Eles são identificados pelo conjunto de valores de seus atributos. Dois objetos de valor com os mesmos atributos são considerados iguais.

- Composição: Eles muitas vezes são usados para representar conceitos que são naturalmente compostos de outros valores menores. Por exemplo, um endereço pode ser um objeto de valor composto por rua, cidade, estado e código postal.

- Sem vida própria: Geralmente, os objetos de valor dependem de uma entidade ou agregação maior para existir. Eles não têm vida própria e são utilizados para descrever aspectos específicos de uma entidade ou agregação.

- Comparação por valor: A igualdade de objetos de valor é determinada pelo valor de seus atributos, não por uma referência de memória. Dois objetos de valor com os mesmos valores em todos os atributos são considerados iguais, mesmo que sejam instâncias separadas.
## Aggregate
- Conjunto de dados associados que tratamos como uma unidade para propósito de mudança de dados.
- Quando temos que juntar dados que são de agregados diferentes vemos que eles são referenciados pode id. Ex: Order(custumer_id,item[])

## Domain Services
- Os Domain Services encapsulam regras de negócios complexas ou operações que não se encaixam bem em nenhum objeto do domínio específico. Eles promovem a coesão ao agrupar operações relacionadas, evitando a dispersão de lógica de negócios em vários objetos de domínio.
- Uma entidade pode realizar uma ação que vai afetar todas as entidades?
- Como calcular algo que cuja as informações constam em mais de uma entidade?
- Quando houver muitos Domain Services em seu projeto, TALVEZ, isso pode indicar que seus agregados estão anêmicos.
- Domain Services são Stateless.

## Repositories
- Repositórios são responsáveis por fornecer uma interface para acessar e persistir objetos de domínio. Eles abstraem o armazenamento e recuperam objetos de domínio, permitindo que a lógica de negócios seja desacoplada de detalhes de armazenamento e acesso a dados.