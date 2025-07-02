# Introdução 

Nesta sessão será demonstrado como as regras do firewall do pfSense funcionam. 

# Regras e Default-Deny

O pfSense segue o princípio de segurança do *default-deny*, ou seja, por padrão é negado qualquer tipo de conexão, a não ser que seja explicitamente especificado, isso garante uma maior segurança, visto que é mais prático permitir apenas os protocolos e portas que serão utilizados, e bloquear todo o resto. Além do princípio do default-deny, ele também é considerado *stateful*, isto significa que não são analisados os pacotes individuais, e sim a conexão que está sendo realizada, ele analisa todas as conexões existentes, e a partir do contexto, considera se um pacote deve ser aceito ou bloqueado caso seja considerado malicioso.

# Estados

Em Status > States é possivel ver os Estados que estão acontecendo em tempo real.

[ foto dos estados]

Aqui é mostrado informações como IP, protocolo e portas utilizadas.

# Teste das Regras do Firewall

Tendo como base as regras apresentadas em [Configurações, ](Configurações/Configurações.md)vamos realizar algumas conexões em IPs e portas específicas e checar caso ela foi permitida ou não, na configuração desse laboratório apenas bloqueios são registrados para evitar inundação de logs.

Aqui, tentaremos.... [Pensar em ideias de conexoes, uma delas pode ser do dmz para a rede interna]


Como podemos ver a conexão teve time-out, vamos analisar em Status > SystemLogs o que aconteceu. 

[ Fotos dos bloqueios do firewall] 

as conexões foram bloqueadas, visto que apenas o protocolo X foi permitido, e as outras conexões também foram bloqueadas por utilizar porta X, Y que não estão permitidas nas regras do firewall. Conexões como ping e conexões comuns utilizando protocolo TCP não aparecem visto que foram permitidas, e apenas bloqueios estão sendo logados.

Com isso, podemos ver um pouco de como funcionam as regras do firewall, o conceito de stateful e foram testados vários tipos de conexões para testar o funcionamento e log das regras.
