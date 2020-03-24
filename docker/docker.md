# Docker Tuto


![](https://github.com/Rijaelto/big_Rata/blob/master/docker/images/dockerlogo.png)

Docker es un sistema de contenedores tremendamente útil que vamos a conocer poco a poco. 

Esto es una guía para uso personal como herramienta de consulta y practica. 


# Indice

<!--ts-->
   * [Desinstalación](#Desinstalación)
   * [Instalar y habilitar](#Instalar-y-habilitar)
   * [Desenmascarar](#Desenmascarar)
   * [ejemplo](#ejemplo)
   * [ejemplo](#ejemplo)
   * [ejemplo](#ejemplo)
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

Hola Mundo
------

Lanzar un hola mundo para saber si está funcionando correctamente

```bash
$ docker run hello-world
```

La salida debería ser algo así:

![](https://github.com/Rijaelto/big_Rata/blob/master/docker/images/helloworld.png)

	
