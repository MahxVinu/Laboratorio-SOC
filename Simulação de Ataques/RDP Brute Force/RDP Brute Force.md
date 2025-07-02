# Introdução
Parar criar o cenário da simulação, primeiro eu considerei a seguinte situação: foi aberto para a internet a porta 3389 (RDP) para se conectar a computadores da rede interna via RDP, utilizando o IP externo, além disso, coloquei a máquina interna com uma senha fraca. Com o kali linux, eu utilizarei a ferramenta Hydra para Brute Force, utilizando de 2 listas (usuários e senhas) que retornam as combinações que funcionaram, após isso eu logarei na máquina via RDP utilizando o FREEDRP. 

> **[AVISO]:** abrir a porta de RDP para rede externa é extremamente inseguro e não deve ser feito, aqui foi criado uma situação em que uma configuração equivocada foi feita, e assim um atacante aproveitou da vulnerabilidade. O recomendado é se utilizar de VPN, que não é do escopo desse projeto.

# Configuração de Port Foward e Regra de Firewall

![image](https://github.com/user-attachments/assets/dc10a0e7-85e8-4907-9498-759eae2b3a3d)
![image](https://github.com/user-attachments/assets/7513510c-beaf-4a82-a7a9-e226463eba15)
Estou permitindo qualquer source externo, com destino sendo a porta 3389 (responsável pelo RDP) e após isso configurei o Port Foward para ao acessar o ip WAN (1.1.1.1) redirecionar para o IP da máquina do Windows Server (IP 10.0.3.200)

# Criação de Regra do Wazuh

Considerando esse contexto de ataque, será criado uma regra de correlação. Regras de correlação consideram mais de um contexto para gerar o alarme, nesse caso, eu considerei que múltiplas falhas de login que no final terminam em um login sucedido uma atividade suspeita de possível utilizaçao de ferramentas automatizadas.

![Screenshot From 2025-07-02 04-39-11](https://github.com/user-attachments/assets/d13ee699-6ae7-45a9-a702-e6db5d472a21)

- Em ordem, a primeira criação é uma regra básica que detecta um login com tipo de logon 10 (RDP) e gera um alerta de nivel 3 que faz parte do grupo "login_ok" que eu utilizarei futuramente.

- A segunda regra considera um intervalo de 60 segundos em que analisa se o alerta de ID 60122 (login falho do Windows) foi ativado 5 vezes ou mais, com o tipo de login 3 ou 10 (por mais que o método seja via RDP, as ferramentas automatizadas ativam um alerta de LogonType 3) e é gerado um alerta customizado,alertando as múltiplas falhas de login.

- A terceira é uma regra de correlação, ela considera um intervalo maior, em que caso a regra 100002 seja repetida mais de uma vez (muito comum visto que essas ferramentas testam milhares de credenciais)e logo depois um login seja sucedido, gera um alerta de um possivel login suspeito. A razão pelo qual isso foi que o alerta além de checar a ativação do alerta 100002, ele também verifica se algum alerta do grupo "login_ok" também existe, isso foi utilizado visto que o Wazuh não permite colocar mais de uma regra em <if_matched_sid></if_matched_sid>.


# Simulação do ataque

Aqui, utilizando o Kali Linux e a ferramenta Hydra, utilizaremos o seguinte comando:

```
hydra -L user.txt -P pass.txt 1.1.1.1 rdp
```

que basicamente chama duas listas salvas no computador com alguns usários e senhas, então eu informo o endereço de IP e o método (RDP). Isso gera o seguinte resultado:

![image](https://github.com/user-attachments/assets/1e7607b5-cca3-4a4d-a620-fc4038bd7b4d)

Hydra encontrou um usuário e senha, agora eu utilizarei essas credenciais para acessar a máquina com o seguinte comando:

```
xfreerdp3 /u:Administrator /p:testpassword123! /v:1.1.1.1
```

![image](https://github.com/user-attachments/assets/f1e57869-7b19-4faf-b502-8041f8d5624b)

Com isso, acessamos com sucesso a máquina interna da rede. 

# Alerta no Dashboard

Aqui, veremos como aparecem os alertas durante o ataque.

## Durante o Brute force com Hydra

![image](https://github.com/user-attachments/assets/94b6acb9-fecf-4185-91bf-784f63313973)


Como podemos ver, o segundo alerta criado foi gerado, devido a alta quantidade de tentativas.

## Ao Conectar-se a Máquina

![image](https://github.com/user-attachments/assets/bfe831d4-022f-49ba-b2f2-340fc7ba168f)

Aqui, após as múltiplas tentativas e um login bem sucedido do atacante, é realizado com sucesso uma conexão, que ativa o primeiro alerta, e por conseguinte preenche todos os requisitos do alerta 3, que é ativado.

Com isso, foi possivel ver uma vulnerabilidade que pode existir em um sistema, um método de ataque, e formas de e alertar e monitorar os acontecimentos.
