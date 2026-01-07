# Projeto Final CCNA 3 - Automação com Ansible

Este repositório contém os scripts de automação para o nosso Exame Final de CCNA 3 (ENSA).

## Entendendo a Estrutura (O que é cada arquivo?)

```bash
ccna3/
├── ansible.cfg
├── inventory
├── playbooks
│   ├── backup.yml
│   └── config-base.yml
└── README.md
```

Como somos novos no Ansible, aqui vai um guia rápido do que está dentro da pasta `ccna3/`:

* **`ansible.cfg`**:
    * É o arquivo de configuração principal. Ele diz pro Ansible onde está o inventário e desativa a verificação chata de chaves SSH.

* **`inventory`**:
    * É a nossa "Agenda de Contatos".
    * **IMPORTANTE:** Aqui ficam os endereços IP dos roteadores (Zagreb, Pula, Split). Se o IP do laboratório mudar, é aqui que alteramos.

* **`playbooks/`**:
    * Aqui estão as "Receitas de Bolo" (o que o Ansible vai fazer).
    * **`backup.yml`**: Conecta em todos os equipamentos, roda o `show running-config` e salva num arquivo de texto no PC.
    * **`config-base.yml`**: Aplica configurações chatas e repetitivas, como **NTP**, **Syslog e SNMP**. (Ou deixamos apenas ate CCNA-2 como config base - exemplo) 

---

## Antes de Começar (Pré-requisitos)

Para isso rodar no seu PC (WSL/Ubuntu), você precisa rodar estes comandos no terminal uma única vez:

```bash
# 1. Atualizar o sistema
sudo apt update

# 2. Instalar o Ansible
sudo apt install ansible -y

# 3. Instalar a "biblioteca" da Cisco (ESSENCIAL)
ansible-galaxy collection install cisco.ios
```
