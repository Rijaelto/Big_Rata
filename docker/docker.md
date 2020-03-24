# Docker Tuto


![](https://github.com/Rijaelto/big_Rata/blob/master/docker/images/dockerlogo.png)

Docker es un sistema de contenedores tremendamente útil que vamos a conocer poco a poco. 

Esto es una guía para uso personal como herramienta de consulta y practica. 


# Indice

<!--ts-->
   * [Desinstalación](#Desinstalación)

<!--te-->


Desinstalación
--------------

```bash
$ sudo apt-get remove docker docker-engine docker.io
```
	
##H2 header Install and enable
------

	sudo apt install docker.io

	sudo systemctl start docker
	sudo systemctl enable docker
	docker --version

Grupo de usuarios
------

	sudo usermod -aG docker $USER
