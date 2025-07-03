# Introdução

Entre as funcionalidades existentes no wazuh, existe a integração com o framework MITRE ATT&CK, que basicamente é uma base de dados acessível a todos, que mapeiam táticas e técnicas (tatics and techniques) que são basicamente objetivos que os atacantes possuem, e os métodos que serão usados.Além disso, existe um mapeamento de diversos grupos de cibercriminosos e quais são seus objetivos e alvos mais comuns.

A partir disso, o wazuh associa os alertas do SIEM com base nas técnicas e táticas que foram mapeados no framework, alertando o analista de SOC em cassos de atividades maliciosas.

> Observação, ter uma técnica associada a um alerta não necessariamente faz ela maliciosa, atividades legítimas como fazer login no windows (T1078: Valid Accounts por exemplo) podem ser marcadas pelo framework. É sempre necessário analisar os alertas com calma e analisando o contexto.

Temos aqui, por exemplo, a matriz Enterprise:
![image](https://github.com/user-attachments/assets/a51711e4-d989-4b2a-8fd2-5f49f00f33eb)

É de suma importância que um analista tenha conhecimento geral das táticas e técnicas para uma melhor visão geral dos eventos que ocorrem na rede.

# Exemplos

Dentro dos próprios alertas existe um campo referente as técnicas e táticas do Framework, aqui estão alguns exemplos

## Exemplo do ataque de Reverse Shell

![Screenshot From 2025-07-03 01-56-12](https://github.com/user-attachments/assets/0a3d1e58-d3f5-455e-98fd-df8ab0dc0493)

Os alertas podem fazer parte de várias táticas ou alertas oa mesmo tempo, dado o escopo que o atacante está explorando

## Exemplo do Active Scanning via Joomscan

![Screenshot From 2025-07-03 01-58-44](https://github.com/user-attachments/assets/17f3bb7a-00e3-4bf1-b49d-5166789b6f27)

Aqui está sendo marcado como uma técnica de network sniffer, com o objetivo (tática) de discovery.

Além disso, o wazuh tem seu próprio módulo de MITRE no Dashboard, em que permite acessar um gráfico que resume a lista de táticas mais usadas, quais agentes estão sendo mais afetados, etc. 

![Screenshot From 2025-07-03 01-59-08](https://github.com/user-attachments/assets/4b6d7ebf-9187-43da-9b3a-f2fdefeea40b)

Além disso, é possivel ver pela própria aba do agente em específico:

![Screenshot From 2025-07-03 02-00-07](https://github.com/user-attachments/assets/ea5b05bc-d8a2-4688-8de7-0a70232ffb01)





