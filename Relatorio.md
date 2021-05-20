# Relatório do projeto de SIRS

Segurança Informática em Redes e Sistemas 2020-2021, segundo semestre

## Autores

*(limite: 1500 palavras)*

**Grupo 6**

*(usar imagens com 150px de altura; com o **rosto enquadrado**)*   
![Henrique Candeias](Henrique_Candeias.jpg) ![João Rodrigues](JoaoRodrigues.png) ![Miguel Gonçalves](Miguel_Goncalves.jpg)

| Número | Nome              | Correio eletrónico                                      |
| -------|-------------------|---------------------------------------------------------|
| 93583  | Henrique Candeias | <mailto:henrique.a.candeias@tecnico.ulisboa.pt>         |
| 93586  | João Rodrigues    | <mailto:joao.pedro.freixo.rodrigues@tecnico.ulisboa.pt> |
| 93602  | Miguel Gonçalves  | <mailto:migueleduardog2000@tecnico.ulisboa.pt>          |

## Introdução

*(escrever descrição sumária, assumindo que o leitor já leu o enunciado)*

## Diagrama de rede

<img width="684" alt="rede_ultima_iteracao" src="https://user-images.githubusercontent.com/71899990/118989303-d6271900-b979-11eb-8b91-f1509965a270.png">

*(se necessário, acrescentar algum texto explicativo)*
Apresentamos, de seguida, os endereços IP atribuídos a cada uma das interfaces (as subredes correspondentes estão na secção seguinte):

| Equipamento             | Interfaces                                    |
| ------------------------|-----------------------------------------------|
| IDS-corporate           | eht0 -> 169.254.2.1                           | 
|                         | eht1 -> 95.92.192.1                           |
| IDS-servicos            | eht0 -> 169.254.3.1                           |
|                         | eth1 -> 95.92.194.1                           |
| Router-Edificio-Central | eth0 -> 169.254.1.1                           |
|                         | eth1 -> 95.92.198.1                           |
|                         | eth2 -> 169.254.4.1                           |
|                         | eth3 -> 169.254.3.2                           |
|                         | eth4 -> 169.254.2.2                           |
| Router-SCADA            | eth0 -> 95.92.204.1                           |
|                         | eth1 -> 169.254.6.1                           |
|                         | eth2 -> 95.92.196.1                           |
|                         | eth3 -> 169.254.5.1                           |
|                         | eth4 -> 95.92.204.3                           |
|                         | eth5 -> 169.254.4.2                           |
| Router-Subestacao-1     | eth0 -> 95.92.204.4                           |
|                         | eth1 -> 169.254.5.2                           |
|                         | eth2 -> 95.92.200.1                           |
| Router-Subestacao-2     | eth0 -> 95.92.204.2                           |
|                         | eth1 -> 95.92.202.1                           |
|                         | eth2 -> 169.254.6.2                           |
| Router-Internet         | eth0 -> 88.60.0.1                             |
|                         | eth1 -> 88.60.2.1                             |
|                         | eth2 -> 88.60.1.1                             |
|                         | eth3 -> 169.254.1.2                           |
| DNS-acdc.pt             | eth0 -> 95.92.194.2                           |
| www.acdc.pt             | eth0 -> 95.92.194.3                           |
| historian.acdc.pt       | eth0 -> 95.92.198.2                           |
| DNS.root                | eth0 -> 88.60.1.2                             |
| DNS.pt                  | eth0 -> 88.60.2.2                             |
| PC-Internet             | eth0 -> 88.60.0.2                             |




## Justificação de opções

### Decisões de implementação da rede

Gama de endereços alocado à Internet: 
88.60.0.0/22 dividido em 3 blocos

| Subrede          | Gama de enderecos                      |
| -----------------|----------------------------------------|
| LAN PC-Internet  | 88.60.0.0 - 88.60.0.255 (88.60.0.0/24) | 
| LAN DNS-root     | 88.60.1.0 - 88.60.1.255 (88.60.1.0/24) | 
| LAN DNS-pt       | 88.60.2.0 - 88.60.3.255 (88.60.2.0/23) | 


Gama de endereços alocados à ICI e às subestações:
95.92.192.0/20 dividido em 8 blocos


| Subrede            | Gama de enderecos                             |
| -------------------|-----------------------------------------------|
| LAN corporate      | 95.92.192.0 - 95.92.193.255 (95.92.192.0/23)  | 
| LAN de servicos    | 95.92.194.0 - 95.92.195.255 (95.92.194.0/23)  | 
| LAN SCADA          | 95.92.196.0 - 95.92.197.255 (95.92.196.0/23)  |
| LAN Data-Historian | 95.92.198.0 - 95.92.199.255 (95.92.198.0/23)  | 
| LAN Subestacao-1   | 95.92.200.0 - 95.92.201.255 (95.92.200.0/23)  | 
| LAN Subestacao-2   | 95.92.202.0 - 95.92.203.255 (95.92.202.0/23)  |
| LAN VPN            | 95.92.204.0 - 95.92.205.255 (95.92.204.0/23)  | 

        
Gama de endereços alocados às ligações link-local:

| Subrede                                 | Gama de enderecos                             |
| ----------------------------------------|-----------------------------------------------|
| LAN ICI-Internet                        | 169.254.1.0 - 169.254.1.255 (169.254.1.0/24)  | 
| LAN R.ED.CENTRAL - IDS-CORPORATE        | 169.254.2.0 - 169.254.2.255 (169.254.2.0/24)  | 
| LAN R.ED.CENTRAL - IDS-SERVICOS         | 169.254.3.0 - 169.254.3.255 (169.254.3.0/24)  |
| LAN R.ED.CENTRAL - ROUTER-SCADA         | 169.254.4.0 - 169.254.4.255 (169.254.4.0/24)  | 
| LAN ROUTER-SCADA - ROUTER SUBESTACAO-1  | 169.254.5.0 - 169.254.5.255 (169.254.5.0/24)  | 
| LAN ROUTER-SCADA - ROUTER SUBESTACAO-2  | 169.254.6.0 - 169.254.6.255 (169.254.6.0/24)  |


  
 

### Decisões de implementação dos serviços

#### ...

## Escolha do IDS

*(identificar e descrever alternativas consideradas)*

*(justificar escolha)*


## Conclusão

*(o que foi alcançado)*

*(pontos fortes, pontos a melhorar)*

*(sugestões para melhorar o projeto em edições futuras)*
