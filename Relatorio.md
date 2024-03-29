# Relatório do projeto de SIRS

Segurança Informática em Redes e Sistemas 2020-2021, segundo semestre

## Autores

**Grupo 6**

![Henrique Candeias](Henrique_Candeias.jpg) ![João Rodrigues](Joao_Rodrigues.jpg) ![Miguel Gonçalves](Miguel_Goncalves.jpg)

| Número | Nome              | Correio eletrónico                                      |
| -------|-------------------|---------------------------------------------------------|
| 93583  | Henrique Candeias | <mailto:henrique.a.candeias@tecnico.ulisboa.pt>         |
| 93586  | João Rodrigues    | <mailto:joao.pedro.freixo.rodrigues@tecnico.ulisboa.pt> |
| 93602  | Miguel Gonçalves  | <mailto:migueleduardog2000@tecnico.ulisboa.pt>          |

## Introdução

Este relatório descreve a implementação de uma infraestrutura crítica de informação, com a finalidade de controlar e proteger a rede elétrica de uma região ou país. Para isso, após uma análise cuidada do enunciado, procedemos à elaboração da rede do sistema assim como a atribuição dos devidos endereços. De seguida, procedemos à implementação de diversos serviços para garantir a segurança e o correto funcionamento de todo o sistema.

## Diagrama de rede

![Topologia da Rede](Topologia_da_Rede.jpg)

Apresentamos, de seguida, os endereços IP atribuídos a cada uma das interfaces (as subredes correspondentes encontram-se de seguida):

| Equipamento             | Interfaces                                    |
| ------------------------|-----------------------------------------------|
| IDS-corporate           | eth0 -> 169.254.2.1                           | 
|                         | eth1 -> 95.92.192.1                           |
| IDS-servicos            | eth0 -> 169.254.3.1                           |
|                         | eth1 -> 95.92.194.1                           |
| Router-Edificio-Central | eth0 -> 169.254.1.1                           |
|                         | eth1 -> 95.92.198.1                           |
|                         | eth2 -> 169.254.4.1                           |
|                         | eth3 -> 169.254.3.2                           |
|                         | eth4 -> 169.254.2.2                           |
| Router-SCADA            | eth0 -> 169.254.6.1                           |
|                         | eth1 -> 95.92.196.1                           |
|                         | eth2 -> 169.254.5.1                           |
|                         | eth3 -> 169.254.4.2                           |
|                         | VPN  -> 95.92.204.1                           |
| Router-Subestacao-1     | eth0 -> 169.254.5.2                           |
|                         | eth1 -> 95.92.200.1                           |
| Router-Subestacao-2     | eth0 -> 95.92.202.1                           |
|                         | eth1 -> 169.254.6.2                           |
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



Gama de endereços alocado à Internet: 

88.60.0.0/22 dividido em 3 blocos

| Subrede          | Gama de enderecos                      |
| -----------------|----------------------------------------|
| LAN PC-Internet  | 88.60.0.0 - 88.60.0.255 (88.60.0.0/24) | 
| LAN DNS-root     | 88.60.1.0 - 88.60.1.255 (88.60.1.0/24) | 
| LAN DNS-pt       | 88.60.2.0 - 88.60.3.255 (88.60.2.0/23) | 



Gama de endereços alocados à ICI e às subestações:

95.92.192.0/20 dino ponto de vista da VPN, o Router-SCADA é como se fosse um collision domainvidido em 8 blocos


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




## Justificação de opções

### Decisões de implementação da rede

Nesta secção pretendemos explicar o porquê das decisões não triviais tomadas ao longo da construção da topologia da rede.

Na primeira interpretação do enunciado, tínhamos a seguinte topologia:

![Topologia_da_Rede_inicial](Topologia_da_Rede_inicial.jpg)
        

* Mesmo tendo pensado nas duas alternativas, decidimos colocar os equipamentos da Internet em subredes diferentes em vez de na mesma subrede;
* O posicionamento do Switch-SCADA e do PC1 (na versão mais recente, PC-SCADA) foi alterado, porque se, por exemplo, a Estacao-SCADA-2 (na versão mais recente, PC-Subestacao-2) pretendesse enviar um pacote para o PC-Eng-1, ao passar pela LAN entre o Router-SCADA e o Router-Edificio-Central, como o Switch-SCADA na verdade é um *collision domain* no Kathara, então funciona como um hub, pelo que o pacote iria chegar também ao PC1 incorretamente;
* Foi colocada uma ligação visível na topologia, de forma a ser representada a VPN, cumprindo os requisitos do enunciado: "A VPN tem dois troços: *router* da subestação 1 - *router* da LAN SCADA e *router* da subestação 2 - *router* da LAN SCADA". Assim, decidimos alocar endereços à VPN dentro da gama atribuída à ICI. 
* Em relação à implementação dos IDSs, pensámos em implementar segundo o enunciado: "Este detetor deve correr num PC que atue como um *switch* de rede" na primeira iteração mas, depois de obter feedback do professor, pareceu-nos melhor implementá-los como um *router*, porque, pelo que percebemos, implementar um switch no Kathara sem ser como um *colision domain* seria mais complicado;
* Em relação às ligações link-local, inicialmente apenas colocámos a que estava dita explicitamente no enunciado mas, depois de perceber melhor o seu propósito (não usar endereços úteis atribuído à rede ICI desnecessariamente) as ligações link-local foram colocadas em todas as ligações diretas entre routers;
* Em relação às ligações físicas entre as sub-estações e o Router-SCADA, foi intuitivo para o grupo implementá-las diretamente ligadas ao Router-SCADA. Depois, apercebemo-nos que havia uma alternativa: as ligações físicas de cada subestação estarem ligadas ao Router-Internet. Esta última opção não nos pareceu muito eficiente de um ponto de vista académico (se calhar num contexto real em termos económicos faria sentido), porque o pacote cifrado pelo cliente VPN teria de fazer um percuso maior para poder chegar ao servidor VPN (Router-SCADA) e, aí, ser decifrado, pelo que mantivemos a decisão inicial.



### Decisões de implementação dos serviços



#### VPN
Este serviço não está funcional devido ao facto de que as permissões que os ficheiros das chaves e dos certificados possuem, no servidor, não serem válidas - alterámos as permissões nos ficheiros da pasta de arranque do routerscada (servidor) mas, mesmo assim, quando a máquina é inicializada, as permissões continuam a ser as antigas. Decidimos prosseguir para outros serviços. Os clientes não estão a funcionar devido a um erro no ficheiro de configuração (client.conf).

<TODO HENRIQUE>
        
#### SSH

Para a implementação deste serviço, foram previamente obtidas as chaves pública e privada do pcinternet, pceng1 e pceng2, com recurso ao comando 'ssh-keygen -t rsa' e guardadas na pasta shared. Criou-se também o ficheiro authorized_keys para o dnsacdcpt e para o wwwacdcpt, contendo as chaves públicas de cada uma das máquinas anteriores, e guardaram-se esses ficheiros também na pasta shared. Nos ficheiros de dnsacdcpt.startup e no wwwacdcpt.startup, inicia-se o serviço ssh, cria-se o utilizador 'admin' com a opção de autenticação por password desativada e copia-se o ficheiro authorized_keys respetivo da pasta shared para o container docker. Nos ficheiros de pcinternet.startup, pceng1.startup e pceng2.startup, copiam-se as chaves previamente criadas na pasta shared para os respetivos containers.
A criação prévia de ficheiros deveu-se ao facto de existir dependências de comandos entre máquinas, e de não se conseguir garantir uma ordem de início entre as mesmas.

#### FIREWALLS

* Assumimos que a Internet é apenas o endereço 88.60.0.0/22.
* No segundo requisito é dito "as máquinas da DMZ não podem comunicar com o resto da rede da ICI" - assumimos que, por exemplo, os PCs da rede ICI não conseguem fazer curl para as páginas contidas no WWWW - e, no quinto requisito, é dito "deve ser possível fazer *ping* entre todas as máquinas da rede ICI..." - pelo que assumimos que é possível que as máquinas da DMZ possam, apenas, fazer *ping* para o resto da rede.
* Embora implementadas, não é possível testar as regras com o DNS, pois não ficou funcional.
* Não fizemos o sexto requisito.
* Assumimos que, nos requisitos do enunciado, o que não está devidamente explicito que é permitido então é bloqueado.

#### HTTPS

Primeiramente,  as páginas foram implementadas com HTTP. De seguida, com o requisito de implementar as páginas com HTTPS, é possível aceder às páginas pessoais dos Engenheiros e à página da ICI através de HTTPS. Na tentativa de aceder às páginas com HTTP, foi implementada a funcionalidade de indicar que, na consola, deja indicado que a página já não se encontra em HTTP, mas sim em HTTPS. Apesar da implementaç destãoa funcionalidade, quando implementámos a firewall bloqueámos o tráfego do HTTP (porto 80) pelo que já não vai aparecer tal sugestão na consola. Em relação aos certificados, que deve ser possível em pelo menos um PC de exemplo, tentámos colocar o certificado gerado no servidor WWW (etc/apache2/certificate/apache-certificate.crt) na pasta etc/ssl/certs do pceng1, para poder fazer o pedido curl sem recurso à flag "-k", mas, contudo, não funciona. Bibliografia: https://techexpert.tips/apache/enable-https-apache/

#### DHCP

De forma a cumprir com os requisitos do enunciado e fornecer endereços IPs dinâmicos aos PCs da LAN corporate, PC da LAN SCADA e PCs das LANs de controlo, foram colocados quatro DHCP servers (um servidor local para cada LAN). Na LAN corporate, SCADA, Subestação 1 e Subestação 2. os DHCP servers foram colocados os no router IDS-corporate, Router-SCADA, Router-Subestacao-1 e Router-Subestacao-2, respetivamente. Como bibliografia, foram seguidos os exemplos disponibilizados no enunciado.

Na parte de implementação de todos os servidores:

* No ficheiro /etc/default/isc-dhcp-server foi colocada qual a interface em que o servidor está disponível para distribuir os endereços dinâmicos;
* No ficheiro /etc/dhcp/dhcpd.conf foram descomentadas as linhas consideradas relevantes: garantir que o DHCP em questão é o único da LAN; qual a subrede e máscara em questão; qual o endereço IP da interface que se pretende colocar o DHCP a funcionar; endereço de broadcast.


## Escolha do IDS


Foram consideradas como alternativas: 
* Em relação ao Data source, foi considerado o HIDS (implementação do IDS numa máquina em específico) mas, ao ler melhor o enunciado, decidimos que o melhor seria implementar o IDS em routers, que estão bem identificados na topologia de rede.

* Em relação ao Detection method, foi considerado o knowledge-based detection (comparação com ataques já conhecidos) mas, por simplicidade, pensámos que seria melhor implementar um IDS que análisasse padrões que são fora do comum.

Critérios para a escolha do NIDS:
* Pretende-se monitorizar em dois pontos da rede, nomeadamente entre dois equipamentos, portanto o mais apropriado é um Network IDS;

 
## Conclusão

Com este projeto, o grupo relembrou muito dos conceitos base aprendidos na cadeira de Arquitetura de Redes - configuração de equipamentos, garantir conectividade numa dada rede - embora de uma forma mais simples (não foi necessãrio, neste projeto, configurar protocolos de routing). Assim, este projeto complementa o que já foi dito porque, para além de garantir conectividade numa rede, é preciso garantir a sua segurança. 

Pontos fortes:
* Conseguimos aplicar o que foi aprendido em laboratório num contexto de projeto;
* Conseguimos implementar quase todas as funcionalidades requeridas;
* Conseguimos implementar funcionalidades não lecionadas na cadeira.


Pontos a melhorar:
* Perdemos muito tempo com erros que à partida não seriam complicados;

Os requisitos da firewall na nossa interpretação, entravam em conflitos uns com os outros.