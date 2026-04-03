# Projeto de Redes: Integração de Três Campi da UTFPR
### Disciplina: AS63D - Redes De Computadores
Este projeto consiste na simulação de uma infraestrutura de rede robusta interligando os campi da **UTFPR** em Cornélio Procópio (CP), Londrina (LD) e Curitiba (CT), centralizados por um provedor de internet (ISP).

## Fundamentos de Cabeamento Estruturado

Para a implementação, foram considerados os seguintes componentes da **Camada Física (Modelo OSI)**:

* **Cabos CAT6:** Utilizados para transmissões de alta velocidade (até 10 Gbps) com alta resistência a interferências.
    * **Straight-through (Direto):** Conexão entre dispositivos diferentes (ex: PC ao Switch).
    * **Crossover (Cruzado):** Conexão entre dispositivos semelhantes (ex: Switch ao Switch).
* **Conectores RJ45:** Padrão Ethernet de 8 pinos.
* **Patch Panel:** Centralização e organização dos cabos para manutenção facilitada.
* **Ativos de Rede:**
    * **Switch (Camada 2):** Encaminhamento de dados via endereços MAC dentro da LAN.
    * **Roteador (Camada 3):** Interconexão de redes distintas via endereços IP.

## Situação-Problema

A proposta visa a interligação de três unidades da UTFPR. Cada campus é subdividido em dois departamentos principais, cada um com **6 estações de trabalho (PCs)**:
1.  **Administrativo (ADM)**
2.  **Tecnologia (TEC)**

Toda a comunicação externa e entre campi é mediada por um **ISP (Internet Service Provider)**.

## Planejamento de Endereçamento (VLSM)

Utilizou-se a segmentação de sub-redes para garantir isolamento e controle de tráfego. Cada sub-rede foi configurada como `/24`, designando uma rede lógica exclusiva para cada departamento.

| Localidade | Departamento | Sub-rede | Máscara |
| :--- | :--- | :--- | :--- |
| **Campus CP** | ADM | `192.168.10.0/24` | `255.255.255.0` |
| **Campus CP** | TEC | `192.168.11.0/24` | `255.255.255.0` |
| **Campus LD** | ADM | `192.168.20.0/24` | `255.255.255.0` |
| **Campus LD** | TEC | `192.168.21.0/24` | `255.255.255.0` |
| **Campus CT** | ADM | `192.168.30.0/24` | `255.255.255.0` |
| **Campus CT** | TEC | `192.168.31.0/24` | `255.255.255.0` |

## Implementação Técnica

### 1. Estrutura por Campus
* Um roteador principal por campus (CP, LD, CT).
* Dois switches por campus (um por departamento).
* Roteamento interno configurado para permitir a comunicação entre ADM e TEC dentro do próprio campus.
  <img width="1616" height="527" alt="image" src="https://github.com/user-attachments/assets/9878ba0e-4255-45c9-a435-f3937364f85e" />

### 2. O Núcleo (ISP)
* Configuração de um roteador central representando o Provedor de Internet.
* Implementação do protocolo **BGP (Border Gateway Protocol)** para simular a troca de rotas entre os sistemas autônomos dos campi.

  <img width="727" height="735" alt="printISP" src="https://github.com/user-attachments/assets/334bc85b-fdf9-45f1-95b0-38c8b0137cec" />


### 3. Comunicação e Testes
* Verificação de conectividade ponta a ponta (End-to-End).
* Testes de **Ping** realizados com sucesso entre computadores de campi diferentes, cruzando a infraestrutura do ISP:

<img width="835" height="570" alt="image" src="https://github.com/user-attachments/assets/2eabbb04-8359-4092-bd1a-08d25de31ffd" />



---
**Ferramenta Utilizada:** Cisco Packet Tracer
