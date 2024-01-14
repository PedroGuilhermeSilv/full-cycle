# Clean Architeture

## Use cases 
- Intenção
- Clareza de cada comportamento do software
- Limites estruturais: tempos que pensar que nossa regra de negócio independe da tecnologia. 
- Inversão de dependência, uma regra de negócio não depende de um banco ou framewwork mas sim de abstrações (interface).

## DTOs
- Trafegar dados entre os limites arquiteturais
- Objeto anêmico, sem comportamento.
- Contém dados tanto de Input quanto de Output