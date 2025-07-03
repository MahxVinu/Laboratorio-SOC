# Introdução

Nessa etapa de testes, testaremos como o Snort alerta e age contra ataques á um servidor Ubuntu na rede DMZ. 

Para saber sobre a ferramenta e configurações veja [aqui](Laboratorio-SOC/Snort/Snort.md)

Na VM do Kali Linux, utilizaremos a ferramenta Jooomscan, capaz de encontrar vulnerabilidades, configurações inadequadas e situações em que o atacante pode comprometer o sistema. 

O comando utilizado será o seguinte:

``` joomscan -u http://1.1.1.1/ ```

Aqui utilizamos o IP da Wan, e o firewall fará o port fowarding para o endereço do nosos servidor Apache2

![Screenshot From 2025-07-02 23-11-51](https://github.com/user-attachments/assets/cbe3e764-b136-486d-89c4-315bd3ebbffd)

Como podemos ver o joomscan falhou em todos os detectores, veremos agora o motivo.

# Alertas
Após executar o comando, os seguintes alertas aparecem no painel do snort: 

![image](https://github.com/user-attachments/assets/98c35ee9-dcba-4d6d-baab-fac59a774ac2)

e como os logs do pfsense estão sendo enviados para o wazuh, e o snort foi habilitado os logs via configuração, podemos ver eles pelo wazuh também: 
![Screenshot From 2025-07-02 23-12-49](https://github.com/user-attachments/assets/18327cf3-6024-4e27-a84a-43a3c0260903)
![image](https://github.com/user-attachments/assets/58c40683-2f82-4e6d-9a83-99720da70d34)


Pela forma que foi configurado, após ataques é bloqueado apenas a orige (o atacante) por um período de 1 hora. 

![image](https://github.com/user-attachments/assets/e4ff05bf-f2fd-4f60-a8f9-981b22aecc96)

Assim, como o DMZ é exposto à internet, é estritamente necessário que a rede consiga alertar e impedir diversos tipos de ataques.


