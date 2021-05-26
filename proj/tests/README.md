TESTE PROGRAMA DE ACESSO À WEB (HTTP)

De forma a testar o funcionamento do curl, de forma a obter as páginas web, foram feitos os seguintes comandos no web server:

* curl -v 'http://95.92.194.3/public/siteEng1.html'
* curl -v 'http://localhost/public/siteEng2.html'
* curl -v 'http://95.92.194.3/public/siteICI.html'

Esperamos, como ouput que, na consola, seja sugerido que o a página foi mudada para HTTPS.


TESTE PROGRAMA DE ACESSO À WEB (HTTPS)

A partir do PCInternet aceder às páginas disponíveis no servidor WWWW:

* curl -k 'https://95.92.194.3/public/siteICI.html'
* curl -k 'https://95.92.194.3/public/siteEng1.html'
* curl -k 'https://95.92.194.3/public/siteEng2.html'

Se funcionasse, de forma a testar que os certificados se encontram no PCEng1 (onde foi guardado o certificado), para fazer o curl sem o '-k':

* curl 'https://95.92.194.3/public/siteICI.html'

TESTE DHCP

1. Após fazer "kathara lstart", anallisar as consolas dos containers que são DHCP servers e DHCP clients e concluir que o DHCP está a funcionar
2. Fazer "ip a" nos DHCP clients e visualizar que foi atribuído um endereço dentro da range estabelecida
3. Fazer ping de um equipamento a outro e ver que funciona:

Na consola do PC SCADA, testar conectividade com o PC Eng1: 
* ping <Endereço IP dinàmico do PC Eng1>

Na consola do PC Subestacao 1, testar conectividade com o PC SCADA: 
* ping <Endereço IP dinâmico do PC SCADA>



TESTE SSH
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


