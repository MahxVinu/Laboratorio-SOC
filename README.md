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

# Configurações: 

Aqui estão listados como foram configurados cada componente: [Configurações das VMs](Configurações/Configurações.md)


# Diagrama da rede

Todas as máquinas estão dispostas da seguinte forma, com seus devidos IPs, Gateways e DNS.

![Diagrama da Rede](https://github.com/user-attachments/assets/e1954d0f-0de8-4324-88f7-b16f91d76740)

# Máquinas da Rede

## Host Windows 10
Máquina Windows 10 integrada ao Active Directory pelo usuário "John Smith" e também enviando os logs para o Wazuh. 

![Screenshot From 2025-06-29 00-55-20](https://github.com/user-attachments/assets/17b44f15-7db2-44ac-a77b-437873aee667)

## Active Directory

Windows Server com Active Directory (domínio soc.lab)

![Screenshot From 2025-06-29 00-50-34](https://github.com/user-attachments/assets/9ed4e703-1d65-4ec0-b078-e3482ad30c5a)


## Máquina de Pentest

Aqui utilizarei o Kali Linux, comumente utilizado para pentestinge será utilizado para demonstrar a ativação de alguns logs e alertas.

![Screenshot From 2025-06-29 00-53-52](https://github.com/user-attachments/assets/d558367d-ec78-43b6-825e-0ad1b25ef4a2)

 
Para a demonstração dos recursos do laboratório, serão realizados as seguintes simulações de ameaças:
- [RDP Brute Force no Active Directory](Simulação%20de%20Ataques/RDP%20Brute%20Force/RDP%20Brute%20Force.md)
- [Reverse Shell no Apache Server](Simulação%20de%20Ataques/Reverse%20Shell/Reverse%20Shell.md)
- [Active Scanning](Simulação%20de%20Ataques/Active%20Scanning/Active%20Scanning.md)

Além disso, será demonstrado os seguintes:
-  [Bloqueios do Firewall](Firewall/Firewall.md)
-  [Alertas do Snort](Snort/Snort.md)
-  [Mapeamento do MITRE ATT&CK pelo Wazuh](MITRE%20ATT&CK/MITRE%20ATT&CK.md)

 

