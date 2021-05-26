TESTE PROGRAMA DE ACESSO À WEB (HTTP)

De forma a testar o funcionamento do curl, de forma a obter as páginas web, foram feitos os seguintes comandos no web server (já não vai funcionar):
* curl -v 'http://localhost/public/siteEng2.html'
* curl -v 'http://localhost/public/siteEng1.html'
* curl -v 'http://localhost/public/siteICI.html'

TESTE PROGRAMA DE ACESSO À WEB (HTTPS)

* curl -k 'https://95.92.194.3/public/siteICI.html'
* curl -k 'https://95.92.194.3/public/siteEng1.html'
* curl -k 'https://95.92.194.3/public/siteEng2.html'

Tentar colocar os certificados no PCEng1 para fazer o curl sem o '-k':

* curl 'https://95.92.194.3/public/siteICI.html' no PCEng1

TESTE DHCP

1. Após fazer "kathara lstart", anallisar as consolas dos containers que são DHCP servers e DHCP clients e concluir que o DHCP está a funcionar
2. Fazer "ip a" nos DHCP clients e visualizar que foi atribuído um endereço dentro da range estabelecida
3. Fazer ping de um equipamento a outro e ver que funciona.

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


