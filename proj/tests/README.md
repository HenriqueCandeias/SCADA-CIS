TESTES PROGRAMA DE ACESSO À WEB (HTTP)

De forma a testar o funcionamento do curl, de forma a obter as páginas web, foram feitos os seguintes comandos no web server:

* curl -v 'http://95.92.194.3/public/siteEng1.html'
* curl -v 'http://95.92.194.3/public/siteEng2.html'
* curl -v 'http://95.92.194.3/public/siteICI.html'

e ver que ná funciona (tráfego bloqueado pela firewall)


TESTES PROGRAMA DE ACESSO À WEB (HTTPS)

A partir do PCInternet aceder às páginas disponíveis no servidor WWWW:

* curl -k 'https://95.92.194.3/public/siteICI.html'
* curl -k 'https://95.92.194.3/public/siteEng1.html'
* curl -k 'https://95.92.194.3/public/siteEng2.html'

Esperamos, como output, que todas as páginas dêm resposta.

Se funcionasse, de forma a testar que os certificados se encontram no PCEng1 (onde foi guardado o certificado), para fazer o curl sem o '-k':

* curl 'https://95.92.194.3/public/siteICI.html'

TESTES DHCP

1. Após fazer "kathara lstart", anallisar as consolas dos containers que são DHCP servers e DHCP clients e concluir que o DHCP está a funcionar
2. Fazer "ip a" nos DHCP clients e visualizar que foi atribuído um endereço dentro da range estabelecida
3. Fazer ping de um equipamento a outro e ver que funciona:

Na consola do PC SCADA, testar conectividade com o PC Eng1: 
* ping <Endereço IP dinàmico do PC Eng1>

Na consola do PC Subestacao 1, testar conectividade com o PC SCADA: 
* ping <Endereço IP dinâmico do PC SCADA>

TESTES FIREWALL

HTTPS

Requisito 1

 Fazer curl de uma página HTTPS desde o PCInternet para o servidor WWW:

* curl -k 'https://95.92.194.3/public/siteICI.html'

Esperamos, como output, que a página em questão seja devolvida.

Fazer SSH desde o PCInternet até uma das máquinas da LAN serviços:

* ssh admin@95.92.194.2

e ver que funciona.

NOTA: O teste ao DNS não funciona, pela sua implementação parcial.

Depois, para mostrar que apenas se pode aceder aos serviços a partir do PCInternt, fazer ping desde o PCInternet a uma máquina da LAN serviços:

* ping 95.92.194.3

e ver que não funciona.

Requisito 2

Fazer um curl de uma página em HTTPS desde o PCEng1 para o servidor WWW:

* curl -k 'https://95.92.194.3/public/siteICI.html'
 
 e ver que não funciona.
 
Fazer um ping desde, por exemplo, o PC SCADA até ao servidor DNS:

* ping 95.92.194.2

e ver que funciona (por causa do Requisito 5)

Requisito 3

Fazer ping desde o PC SCADA até ao PC Subestacao 1:

* ping <Endereço IP dinâmico do PC Subestação 1>

e ver que funciona

Fazer ping desde o PC SCADA até ao PC Subestacao 2:

* ping <Endereço IP dinâmico do PC Subestação 2>

e ver que funciona

Requisito 4

NOTA: O teste ao DNS não funciona, pela sua implementação parcial mas a regra da Firewall está no ficheiro startup do router SCADA.

Requisito 5

Fazer ping desde o PCEng1, por exemplo, o PCInternet:

* ping 88.60.0.2

e ver que funciona

Requisito 6

Não foi realizado.

Requisito 7

Fazer SSH desde o PC SCADA para o WWW:

ssh admin@95.92.194.3

e ver que não funciona (tráfego bloqueado pela firewall)




SSH


TESTES SSH

* cd /home/
* touch test.txt
* scp test.txt admin@95.92.194.2:/home/admin
* scp test.txt admin@95.92.194.3:/home/admin
* ssh admin@95.92.194.2
* cd /home/admin
* ls
* exit
* ssh admin@95.92.194.3
* cd /home/admin
* ls
* exit


