# Introdução

Nessa etapa de testes, testaremos como o Snort alerta e age contra ataques á rede DMZ. 


# Snort

Snort é um projeto open-source IPS/IDS (Intrusion Prevention System/ Intrusion Detection System) que possuem ambas as funcionalidades de analisar e alertas anomalias na rede.Uma série de regras são comparadas com os pacotes recebidos pela rede, gerando alertas, assim como também pode ser feito deploy na rede para impedir esses pacotes e bloquear os atacantes. Suas características principais são as de packet sniffer, packet logger e IPS.

# Configuração 

Snort foi instalado como um Package direto pelo pfSense, e as configurações podem ser vistas [aqui.](Configurações/Configurações.md) Após isso, é criado uma interface para analisar o DMZ, a razão de escolher especificamente o DMZ em vez da rede inteira foi para evitar ruído e falsos positivos.

> Lembre-se que a DMZ está exposta à internet mas  completamente bloqueada de acessar a rede interna ou de acessar o painel do pfSense por motivos de segurança.
# Teste de Active Scanning

Na VM do Kali Linux, utilizaremos a ferramenta Jooomscan, capaz de encontrar vulnerabilidades, configurações inadequadas e situações em que o atacante pode comprometer o sistema. 

O comando utilizado será o seguinte:

```  ```

Após executar o comando, os seguintes alertas aparecem no painel do snort: 

[foto do alerta]


Pela forma que foi configurado, após ataques é bloqueado apenas a orige (o atacante) por um período de 1 hora. 

[foto da regra e do bloqueio]



Assim, como o DMZ é exposto à internet, é estritametne necessário que a rede consiga alertar e impedir diversos tipos de ataques.


