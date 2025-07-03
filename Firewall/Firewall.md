# Introdução 

Nesta sessão será demonstrado como as regras do firewall do pfSense funcionam. 

# Regras e Default-Deny

O pfSense segue o princípio de segurança do *default-deny*, ou seja, por padrão é negado qualquer tipo de conexão, a não ser que seja explicitamente especificado, isso garante uma maior segurança, visto que é mais prático permitir apenas os protocolos e portas que serão utilizados, e bloquear todo o resto. Além do princípio do default-deny, ele também é considerado *stateful*, isto significa que não são analisados os pacotes individuais, e sim a conexão que está sendo realizada, ele analisa todas as conexões existentes, e a partir do contexto, considera se um pacote deve ser aceito ou bloqueado caso seja considerado malicioso.

# Estados

Em Diagnostics > States é possivel ver os Estados que estão acontecendo em tempo real.

![Screenshot From 2025-07-02 23-39-49](https://github.com/user-attachments/assets/920b26f1-2891-4100-9cd4-5ffbb50098b8)

Aqui é mostrado informações como IP, protocolo e portas utilizadas.

# Teste das Regras do Firewall

Tendo como base as regras apresentadas em [Configurações](Configurações/Configurações.md), vamos realizar algumas conexões em IPs e portas específicas e checar caso ela foi permitida ou não, na configuração desse laboratório apenas bloqueios são registrados para evitar inundação de logs.

Aqui, tentaremos uma conexão SSH para o servidor no DMZ, que utiliza a porta 22 (que não está explicitamente permitido nas regras do firewall)

![image](https://github.com/user-attachments/assets/30add9a6-e78d-41b6-bad2-6db317437621)

Como podemos ver a conexão teve time-out, vamos analisar em Status > SystemLogs o que aconteceu. 

![Screenshot From 2025-07-02 23-45-33](https://github.com/user-attachments/assets/e5e676ca-f12f-45bb-98df-d63e8cd7951c)

as conexões foram bloqueadas, visto que apenas o protocolo X foi permitido, e as outras conexões também foram bloqueadas por utilizar porta X, Y que não estão permitidas nas regras do firewall. Conexões como ping e conexões comuns utilizando protocolo TCP não aparecem visto que foram permitidas, e apenas bloqueios estão sendo logados.

Com isso, podemos ver um pouco de como funcionam as regras do firewall, o conceito de stateful e foram testados vários tipos de conexões para testar o funcionamento e log das regras.
