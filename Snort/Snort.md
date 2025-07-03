# Snort
Snort é um projeto open-source IPS/IDS (Intrusion Prevention System/ Intrusion Detection System) que possuem ambas as funcionalidades de analisar e alertas anomalias na rede.Uma série de regras são comparadas com os pacotes recebidos pela rede, gerando alertas, assim como também pode ser feito deploy na rede para impedir esses pacotes e bloquear os atacantes. Suas características principais são as de packet sniffer, packet logger e IPS.

## Configuração
Snort foi instalado como um Package direto pelo pfSense, e apos isso é criado uma interface para analisar o DMZ, a razão de escolher especificamente o DMZ em vez da rede inteira foi para evitar ruído e falsos positivos.

> Lembre-se que a DMZ está exposta à internet mas completamente bloqueada de acessar a rede interna ou de acessar o painel do pfSense por motivos de segurança.

![Screenshot From 2025-07-02 23-05-37](https://github.com/user-attachments/assets/edf18b7f-ecbc-468e-8258-e56bcd2ae62f)

![Screenshot From 2025-07-02 23-08-27](https://github.com/user-attachments/assets/ea0b4842-220a-4ed0-8f2c-b8a5b1e69d72)

![image](https://github.com/user-attachments/assets/167c6d48-f6d8-4c31-8b46-eaca9d5cfcbd)
Foi habilitado a opção de enviar os alertas para o system log do firewall, para serem enviados para o nosso SIEM

![image](https://github.com/user-attachments/assets/29d3d048-14aa-4e75-891b-11eee3f98911)


![image](https://github.com/user-attachments/assets/b64363a4-0747-4731-8e3e-eb5a35000d1f)

![Screenshot From 2025-06-27 23-55-39](https://github.com/user-attachments/assets/ccd66464-ee3a-43aa-9503-1e1127c6aef1)

![image](https://github.com/user-attachments/assets/73cb86c3-9c00-4566-bfe0-1bae79191edf)


Neste projeto eu habilitei todas as categorias de alertas, e habilitei a detecção de port-scan para tentativas de reconnaissance
