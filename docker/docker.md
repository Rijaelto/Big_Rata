# Docker Tuto


![](https://github.com/Rijaelto/big_Rata/blob/master/docker/images/dockerlogo.png)

Docker es un sistema de contenedores tremendamente útil que vamos a conocer poco a poco. 

Esto es una guía para uso personal como herramienta de consulta y practica. 


# Indice

<!--ts-->
   * [Desinstalación](#Desinstalación)
   * [Instalar y habilitar](#Instalar-y-habilitar)

<!--te-->


Desinstalación
--------------

```bash
$ sudo apt-get remove docker docker-engine docker.io
```
	
Instalar y habilitar
--------------------

```bash
$ sudo apt install docker.io
```

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

	sudo usermod -aG docker $USER
