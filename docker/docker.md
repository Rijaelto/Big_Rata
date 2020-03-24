# Docker Tuto


![](https://github.com/Rijaelto/big_Rata/blob/master/docker/images/dockerlogo.png)

Docker es un sistema de contenedores tremendamente útil que vamos a conocer poco a poco. 

Esto es una guía para uso personal como herramienta de consulta y practica. 


# Indice

<!--ts-->
   * [Desinstalación](#Desinstalación)
   * [Instalar y habilitar](#Instalar-y-habilitar)
   * [Desenmascarar](#Desenmascarar)
   * [Grupo de usuarios](#Grupo-de-usuarios)
   * [Hola Mundo](#Hola-Mundo)
   * [Dockerfile](#Dockerfile)
   * [ejemplo](#ejemplo)

<!--te-->


Desinstalación
--------------

```bash
$ sudo apt-get remove docker docker-engine docker.io
```
	
Instalar y habilitar
--------------------

De apt

```bash
$ sudo apt install docker.io
```

Del repo de docker

```bash
$ curl https://get.docker.com -o dockerinstall.sh
$ sudo sh dockerinstall.sh
```

Iniciarlo, puede ser que del error ese de mask.

```bash
$ sudo systemctl start docker
$ sudo systemctl enable docker
$ docker --version
```

Para pararlo

```bash
$ sudo systemctl stop docker
```

Desenmascarar
-------------

```bash
$ sudo systemctl unmask docker
```

Grupo de usuarios
------

Parea evitar tener que andar con los permisos para arriba y para abajo

```bash
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
```

Despues hay que desloguearse y volverse a loguear para que recargue, que seguro que se puede hacer de otra forma, también es verdad eso. Nota: Buscarlo algún día

Hola Mundo
------

Lanzar un hola mundo para saber si está funcionando correctamente

```bash
$ docker run hello-world
```

La salida debería ser algo así:

![](https://github.com/Rijaelto/big_Rata/blob/master/docker/images/helloworld.png)

	
Pasos que sigue
                
1. Se conecta al demonio. 
2. Se descarga de docker hub la imagen.
3. Crea un contenedor partiendo de esa imagen, y el contenedor genera la salida.
4. Esa salida se envía al terminal.
                
----
	
Dockerfile
------

El dockerfile permite construir una imagen, este dockerfile es muy sencillo:

```dockerfile
FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install nginx -y
RUN echo "hello world" > /var/www/html/index.html

EXPOSE 80/tcp

CMD nginx -g 'daemon off;'
```

Es un archivo de texto, pero no tiene ninguna extensión, su nombre es dockerfile y es recomendable no cambiar ese nombre. 


Images
------

Teniendo un dockerfile se puede construir una imagen. Para el ejemplo anterior, cogemos el dockerfile anterior y lo metemos en una carpeta llamada helloworld, despues ejecutamos el siguiente comando.

```bash
$ docker build helloworld
```

Eso sigue los pasos del dockerfile y nos genera la imagen, en este caso, descargando un ubuntu y siguiendo esos pasos.

```bash
$ docker images
```

![](https://github.com/Rijaelto/big_Rata/blob/master/docker/images/images.png)


Es la primera, 153 MB de imagen, nada mal. 

La eliminamos usando el comando por su ID.

```bash
$ docker image rm ae6ac6a54ed8
```

o

```bash
$ docker rmi ae6ac6a54ed8
```

Lo del ID es un rollo, asique creamos la imagen con una etiqueta que nos será más facíl usar. 

```bash
$ docker build -t hello1:latest helloworld
```

Se pueden ver datos de la imagen con 

```bash
$ docker inspect hello1:latest
```


Contenedores
------

Una vez tenemos la imagen, podemos lanzar el contenedor con 

```bash
$ docker create --name hellocontainer hello1:latest
```

Para saber los contenedores activos 

```bash
$ docker ps 
```

y para saber todos los contenedores

```bash
$ docker ps -a
```
![](https://github.com/Rijaelto/big_Rata/blob/master/docker/images/containers.png)


