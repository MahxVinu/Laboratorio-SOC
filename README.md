Estudo prático de SOC com um laboratório com diversos elementos fundamentais para uma proteção ativa.


# Objetivo

Este projeto visa por em prática recursos rotineiros à qualquer analista de segurança. Com isso em mente, configurei diversas máquinas virtuais em uma rede simulada, um firewall com as devidas regras, e um SIEM (Security Information and Event Management) em que os logs de todas as máquinas serão armazenados e indexados, além disso, posicionei um servidor exposto à internet isolado da rede interna (DMZ) nele, um IPS (Intrusion Prevention System) é utilizado para detectar e prevenir ataques mal intencionados.

# Componentes e Softwares

Todos os softwares são gratuitos ou open source, além disso, utilizei sistemas windows e Linux.

Os recursos serão os seguintes:

- 1 Host conectado ao Active Directory (Windows 10)
- Diretório Ativo (AD) Windows Server 2025
- 1 Servidor Apache2 (Ubuntu Server)
- SIEM/XDR Wazuh (RedHat Enterprise 9)
- pfSense (Firewall)
- Snort (IDS/IPS)


# Topologia da rede

Todas as máquinas estão dispostas da seguinte forma, com seus devidos IPs, Gateways e DNS.

