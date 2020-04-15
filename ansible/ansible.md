# Ansible Tuto


![](https://github.com/Rijaelto/big_Rata/blob/master/ansible/images/logo.png)

Ansible es una herramienta de orquestación. 

Esto es una guía para uso personal como herramienta de consulta y practica. 


# Indice

<!--ts-->
   * [Instalar](#Instalar)
   * [Inventario](#Inventario)      
   * [Tareas](#Tareas)
   * [playbooks](#playbooks)   
   * [configurationFile](#configurationFile)
   * [handlers](#handlers)
   * [roles](#roles)
   * [ansible Container](#ansible_container)
   * [ejemplo](#ejemplo)

<!--te-->


Instalar
--------

Agregar el repositorio

```bash
$ sudo add-apt-repository ppa:ansible/ansible
```

Despues instalar con apt

```bash
$ sudo apt update
$ sudo apt install ansible
```

Inventario
----------


El inventario es el conjunto de maquinas que tenemos que aprovisionar, para mi uso personal son el servidor de plex, el ordenador portátil y la raspberry-pi.

Podemos ver que tenemos configurado en la ruta /etc/ansible/hosts

![](https://github.com/Rijaelto/big_Rata/blob/master/ansible/images/hosts.png)

Se pueden definir los servidores y toda la pesca en este sitio. 

Se puede indicar si queremos que se use otro archivo y donde está ese archivo, en la llamada a ansible o en el archivo de configuración.

Para el comando es añadiendo -i nombreArchivo

Además se pueden agregar por bloques, por ejemplo:

[raspas]
raspi1
raspi2
raspi3

[raspas]
raspi[0:3]


Tareas
------


Ansible es declarativo, es decir, le indicamos el estado en el que tiene que quedar la cosa. Esto se pone usualmente en archivos denominados playbooks, pero tambien se puede hacer mediante comandos. 

Las conexiones las hará por SSH, por tanto, es recomendable configurar la autenticación, en cualquier caso, no es imprescindible. 

Aquí el archivo hosts ya está modificado, le haremos un ping al servidor. 


```bash
$ ansible serverPlex -m ping --ask-pass
```

Nos devuelve algo de este estilo.

![](https://github.com/Rijaelto/big_Rata/blob/master/ansible/images/ping.png)

No hay cambios y nos ha devuelto un pong.

Si se pone localhost se hace sobre la misma maquina, en caso de que la maquina no exista nos dará un error.

Con -i se puede indicar una archivo de hosts alternativo. 

```bash
[targets]

local              ansible_connection=local
other1.example.com     ansible_connection=ssh        ansible_user=myuser
other2.example.com     ansible_connection=ssh        ansible_user=myotheruser
```


```bash
$ ansible serverPlex -m ping  -i archivoalternativo.txt --ask-pass
```

La opción -m indica que se usa un modulo.

Si no se indica usa el modulo por defecto shell, que permite ejecutar comandos y devuelve la salida estandar. 

Por ejemplo, podemos asegurarnos que un paquete este instalado. 

```bash
$ ansible local -m apt -a 'name=vlc state=present'
```

Con esto cambiamos de usuario, metemos la clave y si no encuentra vlc, nos lo instalará.

```bash
$ ansible local -m apt -a 'name=vlc state=present' -b -K
```

![](https://github.com/Rijaelto/big_Rata/blob/master/ansible/images/vlc1.png)

Si se ejecuta de nuevo la salida cambia

![](https://github.com/Rijaelto/big_Rata/blob/master/ansible/images/vlc2.png)


```bash
$ ansible local -m apt -s 'name=python3 state=present'
```

Se pueden usar comando con -a


```bash
$ ansible local -a "ls -a"
```




playbooks
---------

Esto permite organizar todas las tareas que queramos que se hagan, son archivos .yml



```bash
---
- hosts: local/all/nombregrupo
- tasks:
  - name: desinstala vlc
    apt: name=vlc state=absent 
	become: true
```

Todo como sudo

```bash
---
- hosts: local/all/nombregrupo
  become: true
- tasks:
  - name: instala vlc
    apt: name=vlc state=present
```

Ejecutamos el primero y desinstala vlc

```bash
$ ansible-playbook playbook1.yml -K
```


```bash
---
- hosts: local/all/nombregrupo
- tasks:
  - name: detiene 
    apt: name=vlc state=absent 
	become: true
```
 
Se le pueden añadir más opciones, como remote_user: 


Instalación con apt:

Este playbook instala algunos paquetes

```bash
---
- hosts: local
  become: true
  tasks:
  - name: instala paquetes
    apt:
      pkg:
        - vlc
        - thunar
        - git
      state: present
```

Copia de archivos.

Esto copia una carpeta dentro de otra.

```bash
---
- hosts: local
  tasks:
  - name: Copia de una carpeta dentro de otra
    copy:
      src: "/home/ernesto/descompresion/Tiny"
      dest: "/home/ernesto/programas/RenomTiny"
```
Y este copiará el contenido de la carpeta en la otra. 


```bash
  - name: Copia del contenido
    copy:
      src: "/home/ernesto/descompresion/Tiny/"
      dest: "/home/ernesto/programas/RenomTiny/"
```

Con esto sincronizamos que es mejor para muchos archivos. 

```bash
  - name: sincronizacion del contenido
    synchronize:
      src: "/home/ernesto/descompresion/Tiny/"
      dest: "/home/ernesto/programas/RenomTiny/"
```

Creación de una carpeta. 

```bash
---
- hosts: local
  tasks:
  - name: Crear carpeta para tiny Total
    file:
      path: "/home/ernesto/programas/TotalTiny"
      state: "directory"  
```

Podriamos indicar grupos para la cartepa y permisos. 

Esto descarga un tar y lo descomprime en una carpeta

```bash
---
- hosts: local
  vars: 
    descompresionPath: "/home/ernesto/descompresion/"
	
  - name: Crear carpeta para descompresion
    file:
      path: "{{ descompresionPath }}tiny"
      state: "directory"   	

  tasks:
  - name: descarga y extraccion de tiny
    unarchive:
      src: https://release.tinymediamanager.org/v3/dist/tmm_3.1.4_linux.tar.gz
      dest: "{{ descompresionPath }}tiny"
      remote_src: yes   
```

La primera de estas modificará una linea del archivo de configuración de fuse y la segunda nos creara un job para cron que monta con rclone una unidad de drive al reiniciar el ordenador.

```bash

- name: allow other in fuse
  become: true
  lineinfile: 
    dest: /etc/fuse.conf
    regexp: '#user_allow_other' 
    line: 'user_allow_other'
    backrefs: yes
    
- name: Montar la carpeta al reinciar
  cron:
    name: "montar gdrive al reiniciar"
    special_time: reboot
    job: "/usr/local/bin/rclone mount gdrive: /home/ernesto/gdrive --allow-non-empty --allow-other --ignore-existing --fast-list --vfs-read-chunk-size 64M --vfs-read-chunk-size-limit off --cache-workers 20 --tpslimit 50 --rc --rc-user=admin --rc-pass=admin --rc-serve --rc-web-gui &"
 
```

Con este buscaremos los archivos ejecutables y les cambiaremos los permisos, esto es basicamente transformar una linea de bash en 30 líneas, pero bueno, supongo que habrá mejores formas de hacerlo.

```bash     
  - name: buscamos los sh
    find:
      paths: 
        - "{{ programasPath }}renomTiny"
        - "{{ programasPath }}totalTiny"
      file_type: file
      patterns: "*.sh"
    register: listaDeEjecutables

  - name: echo lista
    debug:
      msg: "Archivo: {{ item }}"
    with_items: "{{ listaDeEjecutables.files }}"

  - name: maximos permisos a esos archivos
    become: true
    file:
      path: "{{ item.path }}"
      state: file
      owner: ernesto
      mode: "777"
    with_items: "{{ listaDeEjecutables.files }}"

```


 

configurationFile
-----------------

El archivo de configuración

Se puede guardar en la carpeta donde se usa como ansible.cfg, si no, estará el por defecto en /etc/ansible:

El orden de busqueda del archivo es:

* ansible.cfg (in the current directory)
* ANSIBLE_CONFIG (an environment variable)
* .ansible.cfg (in the home directory)
* /etc/ansible/ansible.cfg

https://docs.ansible.com/ansible/2.4/intro_configuration.html

Tiene muchisimas opciones.

https://docs.ansible.com/ansible/2.4/intro_configuration.html

Ejemplo:


```bash
# some basic default values...
[defaults]
inventory = /etc/ansible/hosts  ; This points to the file that lists your hosts

```

Ejemplo:

```bash
[defaults]
inventory = /hosts 
roles_path = /roles
log_path = ansible.log
forks = 2

```

handlers
--------

Los handler permiten añadir tareas según el resultado de otras tareas, por ejemplo, busco una actualización de rclone, y si la hay la instalo, y si eso sucede, entonces monto de nuevo la unidad. 

ansible Container
-----------------


roles
-----

Los roles sirven para añadir un componente de modularidad a los playbook.

Se dividen en carpetas, con la estructura.


```bash
roles/
	basico/
		vlc/
		rclone/
```

El rol es basico y dentro tenemos los playbook que queremos que se ejecuten. 

Dentro de cada carpeta se crea una carpeta llamada tasks y dentro un playbook que se llama main.yml

La estructura de carpetas puede tener otras carpetas, por ejemplo, para almacenar variables. 

Despues lo ejecutariamos desde otro playbook, como el de test.


```bash
---
- hosts: local
  roles:
  - basico
```

Se lanza el playbook y se van ejecutando. 







- name: misc task on ubuntu 18.04 instance
  hosts: "*"
  vars:
    ansible_python_interpreter: /usr/bin/python3
  tasks:
    - debug: var=ansible_host


ln -s /media/ernesto/archivos/ .



