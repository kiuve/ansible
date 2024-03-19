# Guía de Instalación y Configuración de Ansible

Esta guía proporciona instrucciones paso a paso para instalar y configurar Ansible en tu entorno de desarrollo o producción.

## Instalación de Ansible

1. **Sistema Operativo:**
   - Esta guía está destinada para sistemas basados en Unix como Linux y macOS.

2. **Instalación en la Máquina Controladora:**
   - Instala Ansible en la máquina desde la cual administrarás tus servidores. Esta máquina puede ser tu desktop personal u otro servidor designado.
     - En sistemas Ubuntu o Debian:
       ```bash
       sudo apt update
       sudo apt install ansible
       ```

     - En sistemas macOS (con Homebrew):
       ```bash
       brew install ansible
       ```

3. **Verificación de la Instalación:**
   - Después de la instalación, verifica que Ansible esté correctamente instalado ejecutando:
     ```bash
     ansible --version
     ```

## Configuración de Ansible

1. **Creación del Directorio de Proyecto:**
   - Crea un nuevo directorio para tu proyecto de Ansible:
     ```bash
     mkdir mi_proyecto_ansible
     cd mi_proyecto_ansible
     ```

2. **Creación del Inventario:**
   - Crea un archivo `inventory.ini` y especifica las direcciones IP o nombres de host de tus servidores en él:
     ```ini
     [ubuntu_servers]
     server1 ansible_host=192.168.1.101
     server2 ansible_host=192.168.1.102
     ```

3. **Creación del Playbook:**
   - Crea un archivo `playbook.yml` y define las tareas que deseas realizar en tus servidores:
     ```yaml
     ---
     - hosts: ubuntu_servers
       become: yes
       tasks:
         - name: Actualizar todos los paquetes
           apt:
             upgrade: dist
             update_cache: yes
     ```

     **Nota:** Este ejemplo está pensado para actualizaciones en servidores de producción. Asegúrate de adaptar el playbook según tus necesidades específicas.

4. **Configuración de la Clave SSH:**
   - Especifica la ruta de tu clave SSH en el archivo `ansible.cfg` o pasa la clave como argumento al ejecutar `ansible-playbook`.

## Ejecución del Playbook

Para ejecutar el playbook y realizar las tareas definidas en tus servidores, utiliza el comando `ansible-playbook`:
```bash
ansible-playbook -i inventory.ini playbook.yml --private-key=/ruta/a/tu/clave/ssh
