- [Docker](#docker)
  - [Problemas del Desarrollo de Software Profesional](#problemas-del-desarrollo-de-software-profesional)
    - [Construcción](#construcción)
    - [Distribución](#distribución)
    - [Ejecución](#ejecución)
  - [Virtualización](#virtualización)
    - [Problemas de las VM's](#problemas-de-las-vms)
  - [Containerización](#containerización)
  - [Máquina Virtual vs Docker](#máquina-virtual-vs-docker)
  - [Máquina Virtual](#máquina-virtual)
  - [Docker](#docker-1)
  - [Instalación](#instalación)
  - [Play With Docker](#play-with-docker)
  - [¿Cómo funciona Docker?](#cómo-funciona-docker)
    - [Arquitectura de Docker](#arquitectura-de-docker)
      - [Entidades](#entidades)
  - [Contenedores](#contenedores)
  - [DockerHub](#dockerhub)
  - [Comandos](#comandos)
    - [Hola Mundo](#hola-mundo)
    - [Ver contenedores](#ver-contenedores)
    - [Ver información sobre los contenedores](#ver-información-sobre-los-contenedores)
    - [Nombrar Contenedores](#nombrar-contenedores)
    - [Renombrar Contenedores](#renombrar-contenedores)
    - [Eliminar Contenedores](#eliminar-contenedores)
    - [Ejecutar Ubuntu](#ejecutar-ubuntu)
  - [Ciclo de Vida de un Contenedor](#ciclo-de-vida-de-un-contenedor)
  - [Exponiendo Contenedores](#exponiendo-contenedores)
  - [Bind Mounts](#bind-mounts)
    - [Manejar datos de una BD en un Contenedor](#manejar-datos-de-una-bd-en-un-contenedor)
  - [Volúmenes](#volúmenes)
    - [Crear volumen](#crear-volumen)
    - [Crear contenedor con el volumen](#crear-contenedor-con-el-volumen)
    - [Listar Volúmenes](#listar-volúmenes)
    - [Eliminar Volúmenes](#eliminar-volúmenes)
    - [Comandos de Mongo](#comandos-de-mongo)
  - [Insertar y Extraer Datos de Docker](#insertar-y-extraer-datos-de-docker)
    - [Datos en Docker](#datos-en-docker)
  - [Imágenes](#imágenes)
    - [Listar Imágenes](#listar-imágenes)
  - [Construir Imágenes](#construir-imágenes)
    - [Estructura del Dockerfile](#estructura-del-dockerfile)
    - [Capas de una Imagen](#capas-de-una-imagen)
    - [Retaggear una imagen](#retaggear-una-imagen)
    - [Publicar una imagen](#publicar-una-imagen)
  - [Sistema de Capas](#sistema-de-capas)
    - [Capas de un Contenedor](#capas-de-un-contenedor)
  - [Docker en el Desarrollo de Aplicaciones](#docker-en-el-desarrollo-de-aplicaciones)

# Docker
Docker es una tecnología que permite que una aplicación siempre corra en el mismo entorno, incluyendo todas las dependencias necesarias, lo que evita cualquier tipo de conflictos entre versiones. Podemos pasar los contenedores creados a otras personas para que lo corran en su máquina en un servidor.

## Problemas del Desarrollo de Software Profesional

### Construcción
Escribir código es solo una pequeña parte. La construcción de software normalmente es en equipo, y esto trae distintos problemas como:
- Entorno de Desarrollo
- Dependencias
- Entorno de Ejecución
- Equivalencia con Entorno Productivo
- Servicios Externos

### Distribución

El código tiene que transformarse en un artefacto, o varios, que puedan ser transportados a donde tengan que ser ejecutados.
Esto trae algunos problemas como:
- Divergencia de Repositorios
- Divergencia de Artefactos
- Versionado

### Ejecución
La máquina donde se escribe el software siempre es distinta a la máquina donde se ejecuta de manera productiva, por lo que trae algunos problemas como:
- Compatibilidad con el Entorno Productivo
- Dependencias
- Disponibilidad de Servicios Externos
- Recursos de Hardware

> Nota: Docker te permite construir, distribuir y ejecutar cualquier aplicación en cualquier lado. 

## Virtualización

Versión virtual de algún recurso tecnológico, hardware, SO, recursos de red, etc. Permite atacar en simultáneo los 3 grandes problemas del Desarrollo de Software Profesional.

### Problemas de las VM's

- **Peso**: El peso de una VM's es considerable ya que contiene un SO , incluyendo y repitiendo archivos innecesarios, además de alentar el desarrollo.
- **Costo de Administración**: Como es una máquina, igual que una computadora debe ser administrada, ya sea recibiendo actualizaciones, configurando usuarios, instalando aplicaciones, etc.
- **Múltiples Formatos**: Las máquinas virtuales tiene muchos formatos, como VDI, VMDK, VHD, raw, etc, que puede generar problemas de compatibilidad.

## Containerización

Empleo de  ***Contenedores*** para construir y desplegar software, lo que permite estandarizar la manera como se realiza este proceso. Esto trae varias ventajas importantes como:
- Flexibles: Los contenedores pueden almacenar cualquier tipo de aplicación.
- Livianos: Los contenedores reutilizan el Kernel del SO entre ellos, para no repetir archivo ni librerías.
- Portables: Los contenedores se pueden usar de la misma manera, en cualquier máquina.
- Bajo Acoplamiento: Los contenedores son autocontenidos, es decir, tiene todo lo que necesitan para funcionar, sin depender de otro contenedor.
- Escalables: Los contenedores pueden ampliarse fácilmente para adaptarse a los cambios que requiera la aplicación.
- Seguros: Las herramientas que corren contenedores, como Docker, se aseguran que un contenedor solo pueda acceder a las partes del sistema del anfitrión estrictamente necesarias.

![Virtualización vs Contenedores](https://blogs.bmc.com/wp-content/uploads/2018/07/containers-vs-virtual-machines.jpg)

> Nota: A diferencia de una `Máquina Virtual`, que es una `Abstracción del Hardware` y emula toda una computadora (o servidor), un `Contenedor` es una `Abstracción del Software` y éste puede empaquetar el código, el runtime necesario y las dependencias de una aplicación.

## Máquina Virtual vs Docker

## Máquina Virtual

Una máquina virtual tiene la Infraestructura, un Hypervisor y el SO, el cual puede almacenar nuestra aplicación. Sin embargo, esta alternativa tiene muchas cosas innecesarias, y además es pesada y consume memoria RAM.

## Docker

Mantiene la Infraestructura, el SO Host que corre los contenedores, y dentro de él se puede correr las aplicaciones.
Docker corre una imagen de la aplicación (copia) que contiene:
- `OS`: Una distribución de Linux.
- `Software`: Software necesario para que la aplicación funcione correctamente.
- `App`: La aplicación que se encuentra en desarrollo.

La imagen se puede crear basándose en`DockerFiles`, que es una lista de tareas para crear una imagen. Cuando se construye el DockerFile este se convierte en una imagen, y después se utiliza esa imagen para correr el contenedor.

## Instalación

Para instalar Docker en Windows 10, en este caso la versión Home, debemos realizar los siguientes pasos:

1. Ir a > Características de Windows > Activar las casillas de *Plataforma de Hipervisor de Windows, Plataforma de Máquina Virtual, Subsistema de Windows para Linux*
![Paso 1](https://static.platzi.com/media/user_upload/Captura22-8647cbae-8d9b-48ff-97d5-d2528b4d3760.jpg)
2. Seguir el tutorial de Microsoft para [activar el WSL2](https://docs.microsoft.com/en-us/windows/wsl/install-win10).
3. Descargar e Instalar [Docker](https://www.docker.com/get-started) desde la página oficial.
4. Verifica que ya esté instalado Docker desde la terminal de WSL2.
	```batch
	docker --version
	Docker version 20.10.8, build 3967b7d
	```
## Play With Docker
Podemos utilizar un Contenedor Virtual que nos provee Docker en el caso de no poder instalar la versión de Docker en local, sin embargo, solo está disponible por 4 horas. Es muy útil para trabajar rápidamente desde cualquier navegador, la cual contiene una terminal con la que podremos interactuar. Debemos hacer lo siguiente.
1. Registrarse en DockerHub
2. Ingresar a [Play With Docker](https://labs.play-with-docker.com) 

## ¿Cómo funciona Docker?

### Arquitectura de Docker
El corazón de Docker se denomina Docker Daemon (Server), que es un servicio del SO que maneja todas las entidades con las que trabaja Docker, y permite gestionar los contenedores, ya sea creando, editando, configurarlo, escalarlo, destruirlo, etc. *Es el que interactúa con el SO*
La forma en que el Docker Daemon expone una interfaz para comunicarse, es por medio de una REST API. Adicional, es posible comunicarse desde una máquina remota, exponiendo el Docker Daemon *(Hay que tener precaución)*. Encima de la REST API se encuentra el CLI de Docker, que son los comandos que se ejecutan desde el terminal.
Existe el Cliente por Defecto, sin embargo, El Cliente normalmente se configura según la tecnología de la aplicación que se está desarrollando, por ejemplo Python, en el que a través de sintaxis del lenguaje le hablo al Docker Daemon.

#### Entidades
- Contenedores: Donde corren los aplicativos
- Imágenes: Artefactos que usa Docker para empaquetar contenedores
- Volúmenes de Datos: Forma en que Docker permite acceder con seguridad y de manera flexible al sistema de archivos de la máquina anfitrión.
- Redes: Permite a los contenedores comunicarse entre sí o con el mundo exterior.

## Contenedores

Es el concepto más importante en el mundo de Docker. Un contenedor se puede comprender como una máquina virtual liviana, sin embargo, **NO ES LO MISMO**. 

Una máquina virtual corre sobre otra máquina física, y esta contiene un SO, discos, interfaces de red, etc. Un contenedor es una agrupación de procesos que corren nativamente en la máquina pero están aislados del resto del sistema.

Un Contenedor es una _Unidad Lógica_, Una Máquina Virtual es una _Unidad Física_ (Virtualizada). El contenedor está limitado en acciones y recursos según se configure.


## DockerHub

DockerHub es un repositorio de Docker que provee imágenes prediseñadas, donde se puede sacar cualquier imagen que sirva para iniciar.


## Comandos

### Hola Mundo
```batch
docker run hello-world
```
Aquí estaremos ejecutando un contenedor de ejemplo, el cual contiene un texto informativo en su interior.
> Nota: docker run crea un contenedor y luego lo ejecuta

### Ver contenedores
Contenedores corriendo
```batch
docker ps
```
Contenedores existentes
```batch
docker ps -a
```
**Ejemplo**
```batch
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
79bcf5427bff   hello-world   "/hello"   7 minutes ago   Exited (0) 7 minutes ago             vigorous_ardinghelli
276707d196e7   hello-world   "/hello"   2 hours ago     Exited (0) 2 hours ago               quizzical_perlman
```

### Ver información sobre los contenedores
```batch
docker inspect <containerID>
docker inspect <containerName>
```
**Ejemplo**
```batch
docker inspect 79bcf5427bff
docker inspect vigorous_ardinghelli
```
### Nombrar Contenedores
```batch
docker run --name <custom_name> <container_name>
```
**Ejemplo**
```batch
docker run --name hello-docker hello-world
```
El nombre del contenedor es hello-docker
```batch
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
240bcd080f33   hello-world   "/hello"   12 seconds ago   Exited (0) 8 seconds ago              hello-docker
```
> Nota: NO pueden haber 2 contenedores con el mismo nombre en la misma instalación

### Renombrar Contenedores
```batch
docker rename <old_name> <new_name>
```
**Ejemplo**
```batch
docker rename hello-docker hola-docker
```
El nombre del contenedor ahora es hola-docker
```batch
docker ps -a

CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES
240bcd080f33   hello-world   "/hello"   9 minutes ago    Exited (0) 9 minutes ago              hola-docker
```
### Eliminar Contenedores

- Eliminar un contenedor específico
	```batch
	docker rm <container_id>
	docker rm <container_name>
	```
	**Ejemplo**
	```batch
		docker rm hello-docker
	```
- Eliminar un contenedor específico encendido. Forzamos la eliminación.
	```batch
	docker rm -f <container_id>
	docjer rm -f <container_name>
	```
	**Ejemplo**
	```batch
	docker rm -f proxy
	```
- Eliminar todos los contenedores apagados. *Debemos confirmar la eliminación*.
	```batch
	docker container prune
	```
### Ejecutar Ubuntu

```batch
docker run ubuntu
```
Se crea la imagen de Ubuntu, pero no se ejecuta. Para hacerlo usamos el siguiente comando, que activa el *Modo Interactivo* con `-i`, y se abre la consola con `-t`.
> Nota: Ejecutar el comando crea un nuevo contenedor
```batch
docker run -it ubuntu
```
Ahora nos encontramos ejecutando la terminal de Ubuntu, y podemos ver la versión de la distribución.
```batch
root@root:/# cat /etc/lsb-release

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.2 LTS"
```
Se puede verificar que el contenedor está corriendo abriendo otra terminal a parte y usar el comando.

```batch
docker ps

CONTAINER ID   IMAGE     COMMAND   CREATED              STATUS              PORTS     NAMES
1bcf63de6311   ubuntu    "bash"    About a minute ago   Up About a minute             ecstatic_tereshkova
```

## Ciclo de Vida de un Contenedor

Cada vez que un contenedor se inicia, en realidad se ejecuta un `Main-Process` del SO. Este proceso determina si el contenedor está encendido o apagado. Se puede configurar cualquier comando que deseemos como Main-Process de la siguiente forma.
```batch
docker run --name <container_name> -d <image> <command>
```
**Ejemplo**
```batch
docker run --name alwaysup -d ubuntu tail -f /dev/null
```
Para ejecutar un comando en un contenedor que ya está en ejecución usamos.
```batch
docker exec -it <container_name> <command>
```
**Ejemplo**
```batch
docker exec -it alwaysup bash
```
Para cerrar la ejecución de un contenedor debemos matar el Main-Process definido, en Linux podemos buscar el número de proceso que debemos matar para que el contenedor deje de estar en ejecución. 
```batch
root@root:/# docker inspect --format '{{.State.Pid}}' alwaysup
1659
root@root:/# kill 1659
```
En Windows podemos parar la ejecución con el comando
```batch
docker stop <container_id>
docker stop <container_name>
```
**Ejemplo**
```batch
docker stop alwaysup
```

## Exponiendo Contenedores

Cada contenedor tiene su propia interfaz de red virtual, por lo que pueden haber 2 contenedores distintos con el mismo puerto asignado. Para exponer un puerto del contenedor a un puerto de la máquina hacemos lo siguiente.

```batch
docker run --name <container_name> -p <local_port>:<container_port> <image>
```
El flag `-p` significa publish, y permite configurar el puerto que se desea exponer.

**Ejemplo**
```batch
docker run --name proxy -p 8080:80 nginx
```
Si no se usa el Flag `-d` , Docker conecta el Shell a la Salida Estándar de la Imagen, en este caso la imagen de Nginx, y por lo tanto mostrará los Logs en la terminal. No obstante, el puerto estará en funcionamiento y se puede probar en cualquier navegador. Además, cuando se cierren los Logs, también se cerrará el contenedor.

    localhost:8080

Cuando usamos el `-d`, podemos esconder los Logs en la ejecución y la conexión de la imagen con la consola, es decir, podemos seguir escribiendo comandos con el contenedor corriendo. Además, cuando queramos realizar un seguimiento de los Logs, así se cierren los mismos, el contenedor no se va a cerrar.

**Ejemplo**
```batch
docker run --name proxy -d -p 8080:80 nginx
```
Para ver los Logs del contenedor, podemos usar el comando. Aparecerá un listado con todas las peticiones que se han hecho.

```batch
docker logs <container_id>
docker logs <container_name>
```
**Ejemplo**
```batch
docker logs proxy
```
Para ver los Logs a medida que se van generando usamos el comando. *Cerramos el seguimiento con `ctrl + c`*
```batch
docker logs -f <container_id>
docker logs -f <container_name>
```
**Ejemplo**
```batch
docker logs -f proxy
```
Para ver los últimos N Logs .
```batch
docker logs --tail <n_logs> <container_name>
```
**Ejemplo**
```batch
docker logs --tail 10 proxy
```
> Se puede agregar opcionalmente la bandera `-f`, si se desea seguir con el seguimiento de los Logs.

## Bind Mounts

Manejo de Datos en Docker. Los contenedores son entidades auto-contenidas que no pueden acceder al SO anfitrión, a menos que se le permita. Usualmente tenemos datos en alguna otra aplicación que son necesarias de acceder por determinada razón.

### Manejar datos de una BD en un Contenedor

Se crea un Bind Mount, donde se especifica un directorio que contendrá una versión espejo en el local de lo que está en el contenedor.

- Creamos un directorio dentro la carpeta raíz.
	**Ejemplo**
	```batch
	mkdir mongodata
	```
- Especificamos el directorio (ruta absoluta) local, y el directorio en el contenedor nuevo.
	```batch
	docker run --d --name <container_name> -v <local_path>:<container_path> <image>
	```
	**Ejemplo**
	```batch
	docker run --d --name mongodb -v C:\Users\Bryann\Desktop\dockerdata\mongodata:/data/db mongo
	```
> Nota: La ruta en Windows va separada con `\`, en cambio la ruta en el contenedor (Linux) va separada con `/`
- Accedemos al contenedor y creamos una BD
	```batch
	docker exec -it mongodb bash
	root@root:/# mongo
	> use platzi
	> db.users.insert({"name":"Bryann"})
	```
	Podemos ver que la BD está creada
	```batch
	> db.users.find()
	{ "_id" : ObjectId("6121b91516fa3e48c06f3a57"), "name" : "Bryann" }
	```

Ahora podremos eliminar sin problema el contenedor y sin embargo la BD que se creó estará almacenada en el local. Podemos hacer de nuevo la prueba volviendo a crear el contenedor con las mismas especificaciones de antes y ya estará disponible la BD para ser usada en el contenedor. Esto es posible ya que se cargaron los archivos que estaban almacenados en la carpeta, por lo que cada cosa que yo haga en un lado se verá reflejado en el otro. 
> Nota: Aunque es útil este procedimiento, puede acarrear problemas de seguridad.

## Volúmenes

Es la manera MAS ESTÁNDAR de manejar datos en Docker. Ofrece más seguridad a las personas que ejecutan Docker en Entornos Productivos, y es una evolución de los Bind Mounts.
La parte del disco que afectan a los volúmenes en Docker es manejada por Docker, y no ofrece permisos a menos que alguien sea usuario privilegiado.

### Crear volumen
```batch
docker volume create <volume_name>
```
**Ejemplo**
```batch
docker volume create dbdata
```
### Crear contenedor con el volumen
```batch
docker run -d --name <container_name> --mount src=<volume_name>,dst=<route> <image>
```
**Ejemplo**
```batch
docker run -d --name mongodb --mount src=dbdata,dst=/data/db mongo
```
> Nota: Si el volumen no existe, Docker lo crea automáticamente.
> Nota: Después de la coma que separa `src y dst` no puede haber ningún espacio.

### Listar Volúmenes
```batch
docker volume ls
```

### Eliminar Volúmenes
```batch
docker volume rm <volume_name>
```
**Ejemplo**
```batch
docker volume rm datadb
```
Podemos eliminar el contenedor, sin embargo, el volumen seguirá estando almacenado y podemos utilizarlo en un nuevo contenedor creado, además, estará todavía almacenada la BD que se creó anteriormente.

### Comandos de Mongo
```php
# Usar o Crear una BD
> use <database_name>
# Mostrar BD's
> show dbs
# Insertar documento en una colección
> db.users.insert({"key":"value"})
> db.users.insert({"username":"bryanttv", "role": "developer"})
# Ver registros de una colección
> db.users.find()
```

## Insertar y Extraer Datos de Docker

Se puede introducir o extraer Archivos/Directorios de un contenedor de una manera muy sencilla. Debemos tener un contenedor creado, en este caso será sobre una imagen de Ubuntu.

```batch
docker run -d --name copytest ubuntu tail -f /dev/null
```
Creamos un archivo en Windows desde el mismo directorio donde nos encontramos.
```batch
ni test.txt
```
Una vez creado el archivo, vamos a pasarlo de la máquina local (Anfitrión) al contenedor de Docker. Antes de ello, ejecutamos el contenedor y creamos un directorio dentro de él que almacenará el archivo.
```batch
docker exec -it copytest bash
root@root:/# mkdir testing
```
Desde la terminal ejecutamos el comando correspondiente para insertar el archivo
```batch
docker cp <file_path or folder_path> <container_name>:<file_path or folder_path to container> 
```
**Ejemplo**
```batch
docker cp prueba.txt copytest:/testing/test.txt
```
Podemos hacer la operación contraria, es decir, copiar un archivo/directorio desde el contenedor hasta la máquina local.
```batch
docker cp <container_name>:<file_path or folder_path> <file_path or folder_path to local>
```
**Ejemplo**
```batch
docker cp copytest:/testing/ localtesting
```
El directorio `testing` que estaba en el contenedor se copió en la máquina local en un directorio llamado `localtesting`
> Nota: Para usar `cp` no es necesario que el contenedor esté en ejecución.

### Datos en Docker
![](https://i1.wp.com/cdn-images-1.medium.com/max/800/1*bo6IOrBjaHbtkPgTKT08NA.png?w=1170&ssl=1)
- `Host`: Lugar donde Docker está instalado ***(Máquina Anfitriona)***
- `Bind Mount`: Guarda los archivos en la máquina local persistiendo y visualizando estos datos ***(No Seguro)***
- `Volume`: Guarda los archivos en el área de Docker donde Docker los administra ***(Seguro)***
- `TMPFS Mount`: Guarda los archivos temporalmente y persiste los datos en la memoria del contenedor. Cuando el contenedor se para los archivos desaparecen ***(Solo en Linux)***

## Imágenes

Las imágenes permiten solucionar los problemas de Construcción y Distribución. Las imágenes son plantillas o moldes a partir de las cuales Docker crea contenedores. Si se relaciona con el concepto de Programación Orientada a Objetos (POO) podemos ver a las imágenes como una `Clase`, y los contenedores vendrían siendo una `Instancia de la Clase`.

### Listar Imágenes
```batch
docker image ls
docker images
```
```batch
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
nginx         latest    dd34e67e3371   5 days ago     133MB
mongo         latest    269b735e72cb   2 weeks ago    682MB
ubuntu        latest    1318b700e415   3 weeks ago    72.8MB
hello-world   latest    d1165f221234   5 months ago   13.3kB
```
En el listado se puede encontrar información sobre el nombre, el TAG (Versión), el ID, hace cuanto fue creada, y el tamaño.

Para traerse imágenes del repositorio oficial de Docker, Docker Hub, debemos usar el comando pull, especificando solo el nombre de la imagen (trae la versión `latest`), o agregándole la versión que queremos bajar.
```batch
docker pull <image_name>
docker pull <image_name>:<tag_version>
```
```batch
docker pull ubuntu
docker pull ubuntu:18.04
```
> Nota: Cuando descargamos la misma imagen 2 veces, Docker los almacenará con punteros lógicos distintos, sin embargo, será el MISMO CONTENEDOR sin ninguna duplicación.
> Nota: Es necesario crear una cuenta en [DockerHub](https://hub.docker.com)

## Construir Imágenes

El proceso para crear una imagen se basa siempre en un archivo llamado `Dockerfile`. Se parte de este archivo y posteriormente ejecutando el comando `BUILD` el resultado será una imagen. Esta imagen nos servirá para generar infinitos contenedores, ya que es una plantilla.

### Estructura del Dockerfile

Todo Dockerfile inicia con un `FROM`, el cual indica que se está basando de alguna imagen en particular. Todo lo declarado en el Dockerfile se ejecuta en tiempo de Build.

```batch
FROM baseImage
```
**Ejemplo**
```batch
FROM ubuntu:lastest
```
Podemos ejecutar un comando dentro del Shell mediante la sentencia `RUN`
```batch
RUN command
```
**Ejemplo**
```batch
RUN touch /usr/src/hola-docker.txt
```
Una vez escrito el Dockerfile ejecutamos el `BUILD` para crear la imagen.
```batch
docker build -t <base_name>:<tag_image> <build_context>
```
> Cada instrucción en un Dockerfile genera una nueva capa en la imagen resultante.


### Capas de una Imagen

Todas las imágenes son un conjunto de capas o layers. Cuando creamos una nueva imagen estamos apuntando a varias capas. Cada capa nueva es una diferencia con la capa anterior, parecido a Git.

![Capas de una Imagen](https://static.platzi.com/media/user_upload/Screenshot%20from%202020-11-06%2019-53-30-a305c998-0991-44ad-9319-80cacb1a4bc7.jpg)

### Retaggear una imagen
```batch
docker tag <old_image><old_tag> <new_image><new_tag>
docker tag <image>:<tag> <username>/<image>:<tag>
```
> Se puede opcionalmente cambiar el nombre de la imagen y del tag.

**Ejemplo**
```batch
docker tag postgres:latest dbpostgress:20.21
docker tag ubuntu:platzi bryanttv/ubuntu:platzi
```
Cuando cambiamos el Tag podemos observar que se encuentra el antiguo, sin embargo, es la misma y única imagen _(Se ocupa el mismo espacio en disco)_, pero con otro Tag. Los 2 apuntan a la misma capa.

### Publicar una imagen

Primero es necesario iniciar sesión en Docker Hub desde la consola.
```batch
docker login
```
Posteriormente ya se puede publicar la imagen usando un comando típico de Git, el `push`
```batch
docker push <dockerhub_username>/<image>:<tag>
```
**Ejemplo**
```batch
docker push bryanttv/ubuntu:platzi
```
> Docker reutiliza las capas de las imágenes que ya estén en Docker Hub, para así ahorrar espacio y ser mas eficiente. Por ejemplo, en esta imagen publicada Docker reutilizó la imagen de Ubuntu.

> Todas las imágenes publicadas en DockerHub son públicas, a menos que se pague por mantenerla en privado.

## Sistema de Capas
 
 Una imagen es un conjunto de capas, las cuales van una debajo de otra de una manera ordenada. Es fácil entender como está hecha una imagen a partir de su Dockerfile.

Para observar como están construidas las capas de una imagen usamos el comando.
```batch
docker history <name_image><tag_image>
```
**Ejemplo**
```batch
docker history ubuntu:platzi
```
Y mostrará todas las capas que se fueron creando a medida que se construyó la imagen.
```batch
IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
8abe4140147e   27 minutes ago   RUN /bin/sh -c touch /usr/src/hola-docker.tx…   0B        buildkit.dockerfile.v0
<missing>      4 weeks ago      /bin/sh -c #(nop)  CMD ["bash"]                 0B
<missing>      4 weeks ago      /bin/sh -c #(nop) ADD file:524e8d93ad65f08a0…   72.8MB
```
Existe otra forma de ver la construcción de la imagen mediante el uso de una herramienta llamada `dive`, disponible para descargar en su [repositorio](https://github.com/wagoodman/dive) de GitHub *(Windows)*

> Se recomienda añadir la carpeta donde está el dive.exe a las variables de entorno para poder ejecutar el comando `dive`

Usamos el comando
```batch
dive <name_image>:<tag_image>
```
**Ejemplo**
```batch
dive ubuntu:platzi
```
![Dive](https://miro.medium.com/max/2000/0*8Mw53HBdPHshDCdj)

Da una visión mas descriptiva de la imagen.  A la izquierda se muestras las diferentes capas con información importante, y a la derecha se muestran los archivos presenten en cada capa. Se puede pasar de una sección a otra usando el `TAB`. En la sección de los archivos, si usamos el atajo `ctrl +  u`, podemos dejar visible solo los archivos que se modificaron.

> En Docker cada capa es solo un pequeño cambio con respecto al anterior.

> En un comando sería mejor ejecutar las instalaciones de todas las dependencias para poder optimizar el uso del espacio en Docker.

### Capas de un Contenedor

Los contenedores tiene su propia capa mutable (modificable) independiente de las capas inmutables (no pueden ser modificadas una vez sea creada) que pertenecen a la imagen.


## Docker en el Desarrollo de Aplicaciones

- [Docker](#docker)
  - [Problemas del Desarrollo de Software Profesional](#problemas-del-desarrollo-de-software-profesional)
    - [Construcción](#construcción)
    - [Distribución](#distribución)
    - [Ejecución](#ejecución)
  - [Virtualización](#virtualización)
    - [Problemas de las VM's](#problemas-de-las-vms)
  - [Containerización](#containerización)
  - [Máquina Virtual vs Docker](#máquina-virtual-vs-docker)
  - [Máquina Virtual](#máquina-virtual)
  - [Docker](#docker-1)
  - [Instalación](#instalación)
  - [Play With Docker](#play-with-docker)
  - [¿Cómo funciona Docker?](#cómo-funciona-docker)
    - [Arquitectura de Docker](#arquitectura-de-docker)
      - [Entidades](#entidades)
  - [Contenedores](#contenedores)
  - [DockerHub](#dockerhub)
  - [Comandos](#comandos)
    - [Hola Mundo](#hola-mundo)
    - [Ver contenedores](#ver-contenedores)
    - [Ver información sobre los contenedores](#ver-información-sobre-los-contenedores)
    - [Nombrar Contenedores](#nombrar-contenedores)
    - [Renombrar Contenedores](#renombrar-contenedores)
    - [Eliminar Contenedores](#eliminar-contenedores)
    - [Ejecutar Ubuntu](#ejecutar-ubuntu)
  - [Ciclo de Vida de un Contenedor](#ciclo-de-vida-de-un-contenedor)
  - [Exponiendo Contenedores](#exponiendo-contenedores)
  - [Bind Mounts](#bind-mounts)
    - [Manejar datos de una BD en un Contenedor](#manejar-datos-de-una-bd-en-un-contenedor)
  - [Volúmenes](#volúmenes)
    - [Crear volumen](#crear-volumen)
    - [Crear contenedor con el volumen](#crear-contenedor-con-el-volumen)
    - [Listar Volúmenes](#listar-volúmenes)
    - [Eliminar Volúmenes](#eliminar-volúmenes)
    - [Comandos de Mongo](#comandos-de-mongo)
  - [Insertar y Extraer Datos de Docker](#insertar-y-extraer-datos-de-docker)
    - [Datos en Docker](#datos-en-docker)
  - [Imágenes](#imágenes)
    - [Listar Imágenes](#listar-imágenes)
  - [Construir Imágenes](#construir-imágenes)
    - [Estructura del Dockerfile](#estructura-del-dockerfile)
    - [Capas de una Imagen](#capas-de-una-imagen)
    - [Retaggear una imagen](#retaggear-una-imagen)
    - [Publicar una imagen](#publicar-una-imagen)
  - [Sistema de Capas](#sistema-de-capas)
    - [Capas de un Contenedor](#capas-de-un-contenedor)
  - [Docker en el Desarrollo de Aplicaciones](#docker-en-el-desarrollo-de-aplicaciones)