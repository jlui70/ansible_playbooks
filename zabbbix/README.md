# Instalação do Zabbix Completo com Suporte SNMP no Ubuntu 24.04

Este repositório contém o playbook Ansible para instalar o Zabbix completo com suporte a SNMP no Ubuntu 24.04.

## Como Usar

1. **Clone o repositório**:

    Clone o repositório no diretório `/etc/ansible` (ou onde você preferir):

    ```bash
    git clone https://github.com/josezipf/ansible_playbooks.git /etc/ansible
    cd /etc/ansible
    ```

2. **Instalar as Roles do Ansible Galaxy**:

    Antes de rodar o playbook, instale as roles necessárias do Ansible Galaxy:

    ```bash
    ansible-galaxy install josezipf.zabbix7-mysql-ubuntu2404
    ansible-galaxy install josezipf.zabbix7-server-ubuntu2404
    ansible-galaxy install josezipf.zabbix7_frontend_ubuntu2404
    ansible-galaxy install josezipf.zabbix_agent2_v7_snmp
    ```

3. **Editar o Inventário**:

    Abra o arquivo `hosts` localizado em `/etc/ansible/hosts` e adicione ou altere o inventário para refletir os seus servidores de destino.

    Exemplo de inventário (`/etc/ansible/hosts`):

    ```ini
    [zabbix_servers]
    seu_servidor_ansible ansible_connection=local
    ```

4. **Editar o Playbook**:

    Abra o playbook `ansible_playbooks/zabbix/playbook_install_zabbix7_ubuntu2404_mysql.yml` e certifique-se de que o valor de `hosts` está corretamente configurado para o seu inventário. Substitua `local` ou `all` pelo grupo de hosts que você deseja usar.

    Exemplo de playbook:

    ```yaml
    ---
    - name: Instalar Zabbix completo com suporte SNMP no Ubuntu 24.04
      hosts: zabbix_servers  # Substitua por seu grupo de servidores
      become: true
      roles:
        - role: josezipf.zabbix7-mysql-ubuntu2404
        - role: josezipf.zabbix7-server-ubuntu2404
        - role: josezipf.zabbix7_frontend_ubuntu2404
        - role: josezipf.zabbix_agent2_v7_snmp
