# Instalação do Zabbix Completo com Suporte SNMP no Ubuntu 24.04

Este repositório contém o playbook Ansible para instalar o Zabbix completo com suporte a SNMP no Ubuntu 24.04.

## Como Usar

1. **Clone o repositório**:

    ```bash
    git clone https://github.com/josezipf/ansible_playbooks.git
    cd ansible_playbooks
    ```

2. **Instalar as Roles do Ansible Galaxy**:

    Execute os seguintes comandos para instalar as roles necessárias:

    ```bash
    ansible-galaxy install josezipf.zabbix7-mysql-ubuntu2404
    ansible-galaxy install josezipf.zabbix7-server-ubuntu2404
    ansible-galaxy install josezipf.zabbix7_frontend_ubuntu2404
    ansible-galaxy install josezipf.zabbix_agent2_v7_snmp
    ```

3. **Rodar o Playbook**:

    Após instalar as roles, você pode rodar o playbook com o comando abaixo:

    ```bash
    ansible-playbook -i hosts install_zabbix.yml
    ```

> Lembre-se de editar o arquivo `hosts` para refletir os seus servidores.

---

## Licença

Este projeto é de código aberto. Sinta-se à vontade para contribuir ou personalizar conforme necessário.
