# Obligatorio Taller Linux Tallerjulio2024

Para el obligatorio se solicita contar con 3 vm's, de los cuales 1 es un controller centOS, otro se utilizara un servidor centos como servidor web y el ultimo sera un servidor ubuntu para la base de datos utilizando Mariadb.

## Inventario
[centos]
server01 ansible_host=192.168.56.103

[ubuntu]
server02 ansible_host=192.168.56.105

[linux:children]
centos
ubuntu

## GIT
Se instala git y se trae los documentos y claves publicas desde github. Tambien se baja el repositorio para utilizar los Playbooks
```bash
•	dnf install git
•	git config --global user.name “Jose Vendrell”
•	git config --global user.email joselo_43@hotmail.com
•	git clone https://github.com/Jose-Vendrell/Tallerjulio2024.git 
```
En .git/config se visualizara la llave publica con url, se puede editar y colocar por ssh.
 
Se utiliza ssh-copy-id para colocar la llave publica en otros servidores
```bash
 ssh-copy-id <IP>
```
Las claves publicas se crearon sin contraseña.
## Ansible
Para el uso de ansible se necesita instalar y configurar pipx.
```bash
•	dnf install python3-pip
•	pip install pipx 
•	pipx ensurepath 
•	pipx install ansible-core 
•	pipx inject ansible-core 
•	pipx inject ansible-core ansible-lint argcomplete 
•	activate-global-python-argcomplete –user 
•	. /home/sysadmin/.bash_completion 
```
Esto nos permite instalar y gestionar aplicaciones pythone en entornos aislados, ejecutar comandos sin necesidad de especificar la ruta, así como también autocompletados y herramientas para verificar la calidad del código de en los playbooks de Ansible.

Para correr los playbooks se utiliza:
```bash 
ansible-playbook -i inventory/servidores hardening.yml --ask-become-pass
```
Esto realiza una lectura del archivo, ejecuccion del playbook y solicita contraseña sudo para elevar los privilegios. 
Utilizando --syntax-check podremos corroborar que el archvo se encuentra correctamente y sin errores de gramatica o espacios.

# Requisitos Ansible
Para poder trabajar correctamente con los playbooks de este obligatorio, debemos instalar los modulos correspondientes:
```bash
ansible-galaxy collection install –r collections/requirements.yml
```
Collections:
  - name: ansible.posix
  - name: community.general
  - name: community.mysql 

## Webserver
```bash 
ansible-playbook -i inventory/servidores webserver.yml --ask-become-pass
```
Instala httpd (Apache), abre puertos, habilita firewall y configura virtualhost con el archivo virtualhost.conf en /files/virtualhost.conf
## Tomcat
```bash 
ansible-playbook -i inventory/servidores tomcat.yml --ask-become-pass
```
Realiza la instalacion de la herramienta tar, descarga y descomprime tomcat, creando su directorio opt/tomcat, inicia el servicio y copia el archivo todo.war
## Base de datos
```bash 
ansible-playbook -i inventory/servidores database.yml --ask-become-pass
```
Configura el firewall y el trafico del mismo, levanta el servicio e installa maria db. 
Tambien configura la base de datos de la aplicacion y remueve datos de prueba creados por default
## todo.sql
Cuenta con la configuracion de la base de datos todo. Este se encuentra en /Tallerjulio2024/files/todo.sql

## App.properties
El archivo de app properties debe estar en /opt/config/app.properties

```bash
tipoDB=mysql
jdbcURL=jdbc:mysql://192.168.56.105:3306/todo
jdbcUsername=sysadmin
jdbcPassword=tlxadmin
```
## Referencias
### Verificar siempre las versiones para no tener inconvenientes!!!
Mas Modulos de Ansible en:
[Link Ansible modules](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html)

Github profesor de la materia
[Link git emverdes](https://github.com/emverdes/TallerJulio2024)

Corregir syntaxis yml:
[Lector yml](https://yamlchecker.com/)

Creacion documento readme:
[Make a reedme](https://www.makeareadme.com/)

Tambien se utilizo editar directamente de github en README.md
