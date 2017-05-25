# Mini-proyecto Sistema operativos
Felipe Clement - A00320196   
Andrés Villegas - A00239620   
Github del proyecto: https://github.com/avillega/so-project

## Descripción breve de lo solicitado
1. La instalación de Ubuntu Server 16.04 inicio con la descarga del archivo ISO desde la pagina oficial de ubuntu https://www.ubuntu.com/download/server . Luego se procedio a crear la maquina virtual en VirtualBox y se configuraron alli dos interfaces de red, una host-only y otra NAT. No se configuro alli una interfaz Bridge ya que se no se considero necesaria para el desarrollo del proyecto. Para la instalación se procedio siguiendo las instrucciones del wizard de instalación. Entre las más notables diferencias entre la instalación de Centos7 y Ubuntu Server estan : No se configura un password para el usuario root; la interfaz (GUI) es una interfaz por consola; Se hace explicito aceptar la cración de varias particiones en el disco donde se instala el sistema operativo. Una vez instalado se hace el reboot y se inicia la configuración.

2. A diferencia de Centos7, Ubuntu no detecta de forma automatica las interfaces de red que se han configurado via VirtualBox, por tanto no podemos hacer `ifup enp0s...` como estabamos acostumbrados. Para que Ubuntu detecte correctamente la interfaz hay que agregar unas cuantas lineas al archivo `/etc/network/interfaces` este archivo contine la deficinición de las interfaces de red y algo de configuración, por ejemplo, si toma su ip via dhcp. Una vez agregada la interfaz a este archivo es necesario reiniciar el servicio de networking `sudo service networking restart`. Como se puede ver, este servicio tiene un nombre diferente al servicio de Centos& (`network.d`)

3. Por defecto Ubunto server no tiene un firewall instalado, lo cual hace que los puertos ya esten abiertos sin necesidad de configuración extra. Esto a nivel de seguridad es peligroso y se recomienda instalar un firewall

4. A diferencia de Centos7, Ubunto 16.04 tiene instalad0 Python 3 por defecto y tambien es el python que se ejecuta por defecto. Por tanto, es necesario instalar PIP3 en lugar de PIP tradicional. Para esto se ejecunta el comandos:
```
# apt install python-devel gcc python3-pip

```
Una vez instalado PIP procedemos con la instalación de virtualenv y virtualenvwrapper, cabe aclarar que para el correcto funcionamiento de las instalaciones es necesario usar el comando pip3 en lugar de solo pip. 

5. Para el uso de ambientes virtuales se uso virtuaalenvwrapper. Para que este funcione correctamente es necesario agregar dos lineas al final del archivo `~/.bashrc` 

```
export WORKON_HOME = ~/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh
```
Notese que a diferencia de Centos7 virtualenvwrapper fue instalado en `/usr/local/bin/` en lugar de `/usr/bin/`.   
Una vez hecho lo anterior se debe ejecutar el comando 
```
source ~/.bashrc
```
Para que todos los cambios surtan efecto. De aqui en adelante el trabajo con los ambientes virtuales se reduce a los comandos
```
workon {nombre del ambiente}
deactivate
mkvirtualenv {nombre del ambiente}
```
Una vez dentro del ambiente es necesario instalar todas las dependencias para que la aplicacion desarroallada para el segundo parcial funcione correctamente estas dependencias son:
```
flask
flask-sqlalchemy
flas_restplus
psutil
sqlite
```
Todas estas dependencias se instalan a travez de pip3, exceptuando sqlite que se instala a travez de apt

6. Para hacer uso de la aplicación en python se clono el repositorio de github: https://github.com/avillega/so-exam2.git y se cambio la ruta de la base de datos sqlite, a una dentro del path del proyecto.

7. Por ultimo, se adjunta una captura de netstat que muestra la ejecucion del app en el puerto 8080
![captura netstat](https://rawgit.com/avillega/so-project/master/A00320196-A00239620/resources/netstatCaptura.png)

8. Se sube una imagen gif donde se muestra el funcionamiento de la aplicación
![gif app](https://rawgit.com/avillega/so-project/master/A00320196-A00239620/resources/video_final.gif)
