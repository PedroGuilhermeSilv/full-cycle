# Clean Architeture
- Limites estruturais: tempos que pensar que nossa regra de negócio independe da tecnologia. 
- Inversão de dependência, uma regra de negócio não depende de um banco ou framewwork mas sim de abstrações (interface).

## Use cases 
- Intenção.
- Clareza de cada comportamento do software.

## DTOs
- Trafegar dados entre os limites arquiteturais.
- Objeto anêmico, sem comportamento.
- Contém dados tanto de Input quanto de Output.

## Presenters
- Objetos de transformações.
- Adequa o DTO de output no formato correto para entregar o resultado.

## Entites
- Regras de negócio.
- Se aplicam em qualquer situação.

[Python Clean Architeture](https://pages.github.com/).