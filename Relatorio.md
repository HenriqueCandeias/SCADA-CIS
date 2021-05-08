# Relatório do projeto de SIRS

Segurança Informática em Redes e Sistemas 2020-2021, segundo semestre

## Autores

*(limite: 1500 palavras)*

**Grupo 6**

*(usar imagens com 150px de altura; com o **rosto enquadrado**)*   
![Henrique Candeias](Henrique_Candeias.jpg) ![João Rodrigues](22222-bob.png) ![Miguel Gonçalves](33333-charlie.png)

| Número | Nome              | Correio eletrónico                                      |
| -------|-------------------|---------------------------------------------------------|
| 93583  | Henrique Candeias | <mailto:henrique.a.candeias@tecnico.ulisboa.pt>         |
| 93586  | João Rodrigues    | <mailto:joao.pedro.freixo.rodrigues@tecnico.ulisboa.pt> |
| 93602  | Miguel Gonçalves  | <mailto:migueleduardog2000@tecnico.ulisboa.pt>          |

## Introdução

*(escrever descrição sumária, assumindo que o leitor já leu o enunciado)*

## Diagrama de rede

*(usar imagem com qualidade)*

*(se necessário, acrescentar algum texto explicativo)*

## Justificação de opções

### Decisões de implementação da rede

Gama de endereços alocado à Internet: 
88.60.0.0/22 dividido em 3 blocos

LAN PC-Internet :  88.60.0.0 - 88.60.0.255 (88.60.0.0/24)
LAN DNS-root:      88.60.1.0 - 88.60.1.255 (88.60.1.0/24)
LAN DNS-pt:        88.60.2.0 - 88.60.3.255 (88.60.2.0/23)

Gama de endereços alocados à ICI:
95.92.192.0/20 dividido em 9 blocos

LAN corporate:         95.92.192.0 - 95.92.193.255 (95.92.192.0/23)
LAN services:          95.92.194.0 - 95.92.195.255 (95.92.194.0/23)
LAN SCADA:             95.92.196.0 - 95.92.197.255 (95.92.196.0/23)
LAN data-historian:    95.92.198.0 - 95.92.199.255 (95.92.198.0/23)
LAN SCADA-sub-e1:      95.92.200.0 - 95.92.201.255 (95.92.200.0/23)
LAN SCADA-sub-e2:      95.92.202.0 - 95.92.203.255 (95.92.202.0/23)
LAN sub-e1:            95.92.204.0 - 95.92.205.255 (95.92.204.0/23)
LAN sub-e2:            95.92.206.0 - 95.92.206.255 (95.92.206.0/24)
LAN ICI-Internet:      95.92.207.0 - 95.92.207.255 (95.92.207.0/24)


### Decisões de implementação dos serviços

#### ...

## Escolha do IDS

*(identificar e descrever alternativas consideradas)*

*(justificar escolha)*


## Conclusão

*(o que foi alcançado)*

*(pontos fortes, pontos a melhorar)*

*(sugestões para melhorar o projeto em edições futuras)*
