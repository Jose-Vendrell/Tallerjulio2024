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
Se instala git y se trae los documentos y claves publicas desde github
```bash
•	dnf install git
•	git config --global user.name “Jose Vendrell”
•	git config --global user.email joselo_43@hotmail.com
•	git clone https://github.com/Jose-Vendrell/Tallerjulio2024.git 
```
En .git/config se visualizara la llave publica con url, se puede editar y colocar por ssh. 

## Ansible
Para el uso de ansible se necesita instalar y configurar pipx.
