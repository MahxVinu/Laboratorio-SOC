## pfSense

pfSense é um programa de código aberto com o objetivo de ser usado como roteador e firewall, com uma interface simples de utilizar, e vários recursos adicionais, neste projeto utilizarei syslog-ng e snort.

![Screenshot From 2025-06-29 00-50-25](https://github.com/user-attachments/assets/6e9d0779-7f63-489c-9c49-9d78bef7977e)

As interfaces e seus respectivos IPs

### NAT Outbound

![Screenshot From 2025-06-27 23-48-16](https://github.com/user-attachments/assets/4359814b-61da-48d7-aee1-87d8eb2cbf37)

Aqui é feito o NAT, responsável em converter os endereços privados da rede para o endereço de WAN (neste projeto, 1.1.1.1)

### Regras:

### WAN:

![Screenshot From 2025-06-27 23-44-10](https://github.com/user-attachments/assets/53cf1e5d-50ad-43ae-8532-b9e1e05563ac)

Apenas o NAT e a regra padrao do pfSense ao selecionar bloqueios de conexões de endereço Bogon.
### LAN

![image](https://github.com/user-attachments/assets/b5e7cce2-bc15-41a9-bcbe-eb817c87140a)

Aqui, estão as regrãs de anti-lockout, e 2 regras criadas, uma que permite o ping (protocolo ICMP) e a outra permite navegação básica na internet apenas permitindo protocolos TCP e UDP, nas portas 443, 80, 8080, e 53 (estão sendo referidas como o Alias "Browsing".

### DMZ

![image](https://github.com/user-attachments/assets/d79ac54d-c8dd-4b89-a24a-8f9431d8077b)

Definição de regras corretas no DMZ são de extrema importância, nesse caso, as regras criadas foram as seguintes:

- Bloquear o DMZ de acessar o painel do pfSense
- Bloquear o Acesso do DMZ para a rede LAN interna
- Permitir o Acesso do DMZ ao exterior

### Port Fowarding
Nesse caso, criei um port foward que permite acessar ao servidor (DMZ) acessando o endereço da WAN (1.1.1.1) utilizando protocolo TCP via porta HTTP.

![image](https://github.com/user-attachments/assets/9d54e0fa-e47f-4789-affe-73ffe740eed5)

### Configuração do Syslog-ng 

A razão que utilizei o syslog-ng nesse projeto é pelo fato da estrutura do log do pfsense não ser detectada pelos Decoders padrões do Wazuh (responsável pelo parsing) contudo, o syslog-ng permite que sejam enviados logs no padrão correto que são decodificados pelo Wazuh corretamente. Utilizei como alternativa á criar um decoder próprio por ser mais prático, e também pela possibilidade de encriptar o envio do syslog (não possível no método convencional)

![Screenshot From 2025-06-27 23-49-07](https://github.com/user-attachments/assets/e26504ca-6186-4c7b-b45e-45a4f964367a)

### Envio de Logs via Syslog

![Screenshot From 2025-06-27 23-56-33](https://github.com/user-attachments/assets/08784d1b-cba9-4c82-bcd2-98ecbbed4ebf)

Aqui, habilitei o envio dos logs via Syslog para a porta 5140, porta do syslog-ng , que irá enviar os logs para o wazuh via porta 514.


### Configuração Snort

![Screenshot From 2025-06-27 23-55-39](https://github.com/user-attachments/assets/ccd66464-ee3a-43aa-9503-1e1127c6aef1)
![image](https://github.com/user-attachments/assets/73cb86c3-9c00-4566-bfe0-1bae79191edf)

Neste projeto eu habilitei todas as categorias do wauzh, e habilitei a detecção de port-scan para tentativas de reconnaissance



## Wazuh

Wazuh além de um SIEM (Security Information and Event Management) responsável por agregar logs, criar alertas e monitoramento em tempo real de hosts, ele é considerado um XDR (Extended Response Detection) por recursos adicionais como coletar telemetria de múltiplas camadas, mapeamento com o MITRE ATT&CK e vários Compliances, além de respostas automatizadas.

## Painel Principal

![Screenshot From 2025-06-27 23-54-13](https://github.com/user-attachments/assets/7f0af3b7-2932-45cd-9427-07795990a7a3)

## Agentes

![Screenshot From 2025-06-27 23-54-13](https://github.com/user-attachments/assets/b74d5bce-5e4a-419a-b267-b3c3805ee64d)
