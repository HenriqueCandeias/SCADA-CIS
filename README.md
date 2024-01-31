Group project for Técnico's "Network and Computer Security" BSc course. Grade: 16.9/20.

Skills: **Linux Administration**, **Network Security and Architectures**, **Container Deployment**.

This project consisted of configuring the critical information infrastructure for a cyber-physical system - more specifically, the information system used by a country-wide electricity supplier. The network's structure was designed and implemented such that communications to the internet and specific remote machines could be performed securely. The Figure below represents the system, which was developed in a laboratory environment using [Kathará](https://www.kathara.org/) - a container-based network emulation system. 

![Network Topology](https://github.com/HenriqueCandeias/sirs-g6/blob/main/Topologia_da_Rede.jpg)

In sum, we designed and configured the network's routing and IP addressing (the latter using DHCP for some of the machines), as well as additional security mechanisms, such as SSH communications (using OpenSSH), Firewalls with DMZs, and HTTPS communication to access a web application (in theory, used to control the electricity cyber-physical systems). VPN connections (using OpenVPN) and Snort (a Network Intrusion Detection System - NIDS) were also partially configured.

This assignment's report can be read (in Portuguese) at [Relatorio.md](https://github.com/HenriqueCandeias/sirs-g6/blob/main/Relatorio.md)
