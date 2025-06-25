# Instalação do Zabbix Completo com Suporte SNMP no Ubuntu 24.04

Este repositório contém o playbook Ansible para instalar o Zabbix completo com suporte a SNMP no Ubuntu 24.04.

## ⚠️ Aviso Importante

**As roles utilizadas neste playbook fazem a instalação de um MySQL zerado.**  
Se você já possui um MySQL instalado, **não recomendamos utilizar este playbook**, pois as roles irão alterar a senha do usuário `root` do MySQL e podem sobrescrever configurações existentes. Certifique-se de utilizar este playbook em um ambiente onde o MySQL possa ser instalado ou reinstalado sem impactar outros serviços.

**O sistema operacional deve ser Ubuntu 24.04 e deve estar completamente zerado**, ou seja, sem nenhum outro serviço rodando. Este playbook foi projetado para configurar o Zabbix do zero, e a instalação de outros serviços pode interferir no processo. **Evite usar em servidores com outros serviços ou configurações pré-existentes.**

## Como Usar

1. **Clone o repositório**:

    Clone o repositório no diretório `/etc/ansible` (ou onde você preferir):

    ```bash
    cd /etc/ansible
    git clone https://github.com/josezipf/ansible_playbooks.git
    ```

2. **Instalar as Roles do Ansible Galaxy**:

    Antes de rodar o playbook, instale as roles necessárias do Ansible Galaxy:

    ```bash
    ansible-galaxy install josezipf.zabbix7-mysql-ubuntu2404
    ansible-galaxy install josezipf.zabbix7-server-ubuntu2404
    ansible-galaxy install josezipf.zabbix7_frontend_ubuntu2404
    ansible-galaxy install josezipf.zabbix_agent2_v7_snmp
    ansible-galaxy install josezipf.hardening_zabbix_web
    ansible-galaxy install josezipf.apache2_https_mkcert
    ```

3. **Editar o Inventário**:

    Abra o arquivo `hosts` localizado em `/etc/ansible/hosts` e adicione ou altere o inventário para refletir os seus servidores de destino.

    Exemplo de inventário (`/etc/ansible/hosts`):

    ```ini
    [zabbix_servers]
    seu_servidor
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
        - role: josezipf.apache2_https_mkcert
        - role: josezipf.hardening_zabbix_web
    ```

5. **Rodar o Playbook**:

    Após editar o inventário e o playbook, execute o playbook com o seguinte comando:

    ```bash
    ansible-playbook -i /etc/ansible/hosts ansible_playbooks/zabbix/playbook_install_zabbix7_ubuntu2404_mysql.yml
    ```
    Funcionou com este comando devido usuario ssh com pwd:

   sudo ansible-playbook -i /etc/ansible/hosts ansible_playbooks/zabbix/playbook_install_zabbix7_ubuntu2404_mysql.yml --ask-become-pass

    > Lembre-se de substituir `/etc/ansible/hosts` pelo caminho do seu inventário, caso não esteja usando o padrão.

---

## Licença

Este projeto é de código aberto. Sinta-se à vontade para contribuir ou personalizar conforme necessário.
