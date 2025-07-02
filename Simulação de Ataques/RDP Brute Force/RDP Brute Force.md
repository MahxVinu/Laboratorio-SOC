# Situação Inicial

Parar criar o cenário da simulação, primeiro eu considerei a seguinte situação: foi aberto para a internet a porta 3389 (RDP) para se conectar a computadores da rede interna via RDP, utilizando o IP externo, além disso, coloquei a máquina interna com uma senha fraca. Com o kali linux, eu utilizarei a ferramenta Hydra para Brute Force, utilizando de 2 listas (usuários e senhas) que retornam as combinações que funcionaram, após isso eu logarei na máquina via RDP utilizando o FREEDRP. 

> **[AVISO]:** abrir a porta de RDP para rede externa é extremamente inseguro e não deve ser feito, aqui foi criado uma situação em que uma configuração equivocada foi feita, e assim um atacante aproveitou da vulnerabilidade. O recomendado é se utilizar de VPN, que não é do escopo desse projeto.

# Configuração de Port Foward e Regra de Firewall

![image](https://github.com/user-attachments/assets/dc10a0e7-85e8-4907-9498-759eae2b3a3d)
![image](https://github.com/user-attachments/assets/7513510c-beaf-4a82-a7a9-e226463eba15)
Estou permitindo qualquer source externo, com destino sendo a porta 3389 (responsável pelo RDP) e após isso configurei o Port Foward para ao acessar o ip WAN (1.1.1.1) redirecionar para o IP da máquina do Windows Server (IP 10.0.3.200)

# Criação de Regra do Wazuh

Considerando esse contexto de ataque, será criado uma regra de correlação. Regras de correlação consideram mais de um contexto para gerar o alarme, nesse caso, eu considerei que múltiplas falhas de login que no final terminam em um login sucedido uma atividade suspeita de possível utilizaçao de ferramentas automatizadas.

![image](https://github.com/user-attachments/assets/b8e05d46-921e-4281-9abe-69cc6096f0e5)

- Em ordem, a primeira criação é uma regra básica que detecta um login com tipo de logon 10 (RDP) e gera um alerta de nivel 3 que faz parte do grupo "login_ok" que eu utilizarei futuramente.

- A segunda regra considera um intervalo de 60 segundos em que analisa se o alerta de ID 60122 (login falho do Windows) foi ativado 5 vezes ou mais, com o tipo de login 3 ou 10 (por mais que o método seja via RDP, as ferramentas automatizadas ativam um alerta de LogonType 3) e é gerado um alerta customizado,alertando as múltiplas falhas de login.

- A terceira é uma regra de correlação, ela considera um intervalo maior, em que caso a regra anterior seja repetida mais de 1 vez (muito comum visto que essas ferramentas testando milhares de credenciais) e após isso, um login seja sucedido, gera um alerta alertando um login suspeito. A razão pelo qual isso foi alcançado foi o grupo "login_ok", o Wazuh não permite colocar mais de uma regra em <matched_sid></matched_sid>, então o <if_group></if_group> analisa se algum alerta foi gerado anteriormente em que faz parte desse grupo.
