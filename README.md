PhpIpam - Install
=========

Este Rol instalara la versión que se desea del software phpipam en un sistema Debian BookWorm.
Se instalaran todos los paquetes necesarios para correr el software, dejando un entorno LAMP(Linux Apache MySQL PHP) operativo.
- Configura un virtual-host apache para exponer la aplicación.
- Clona del repositorio oficial el proyecto [phpipam](https://github.com/phpipam/phpipam.git), brindando la posibilidad de indicar la versión en las variables del rol. 
- Crea la DB con sus respectivo usuario y importa el esquema de la misma.
- Modifica los archivos de configuración necesarios del Software Phpipam


Role Variables
--------------

Descripción de las variables principales, para implementar este rol. Las siguientes varaibles son publicadas en el directorio **defautls/main.yml** :

Indicamos la rama que nos basaremos para clonar el poryecto:

```
GIT_VERSION: "master"
```

Definimos los datos para nuestra base de datos, usuario, passwor y nombre de la base de datos:

```
db_user: "phpipam"
db_pass: "phpipamadmin"
db_name: "phpipam"
```

Definimos los datos necesario para configurar el servicio web.


```
app_user: "www_data"
http_port: 80
http_site_conf: "phpipam.conf"
server_admin: "test@dominio.com"
http_fqdn: phpipam.dominio.lan
http_root_site: phpipam
```

Por otro lado las variables declaradas en **vars/main.yml**. En dicho archivo delcaramos todos los paquetes necesarios para que este sistema funcione correctametne.

Para ello utilizamos varias listas de variables, para agrupar los paquetes necesarios devididas en 4 listas:

- apache2
- php
- mysql
- systemconfig


Dependencies
------------

Este rol depende de la colección **community.mysql**, es necesaria instalar esta antes de poder ejecutar este rol:

```
ansible-galaxy collection install community.mysql
```

Esta colección tambien necesita los siguietnes paquetes para su correcto funcionamiento:

- PyMySQL (Python 2.7 and Python 3.x)
- mysql (command line binary)
- mysqldump (command line binary)

Fuentes: 
- [ansible-collections-community-mysql-mysql-db-module-requirements](https://docs.ansible.com/ansible/latest/collections/community/mysql/mysql_db_module.html#ansible-collections-community-mysql-mysql-db-module-requirements)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
---
- name: Instalación y configuración de PHPipam
  hosts: test-host.tudominio.com
  remote_user: root
  become: true

  roles:
   - role: phpipam-install
     tags:
       - phpipam-install

```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
