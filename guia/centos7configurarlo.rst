Instalar CentOS 7 y Configurarlo
==============================

Aquí no vamos a explicar como se instala CentOS7, pero si los requisitos para que funcione nuestro laboratorio
Asegurar estos prerrequisitos

Nuestra maquina virtual le vamos a llamar **CDC01**


Aseguremos una IP fija. en este laboratorio la IP sera 192.168.1.100.

Deshabilitar Selinux::

	# sed -i -e 's/enforcing/disabled/g' /etc/sysconfig/selinux

Deshabilitar el Firewall::

	# systemctl disable firewalld && systemctl stop firewalld

Cambiar nombre del Host::

	# hostnamectl set-hostname cdc01

**Configurar el nombre del HOST y su IP en el archivo /etc/hosts**::

	# vi /etc/hosts
	127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
	::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
	192.168.1.100	cdc01

**Configurar el protocolo X11** para tener operativo el ssh -X y tener la variable DISPLAY activa.

Instalando xorg-x11-server-Xorg.x86_64.::

	# yum -y install xorg-x11-server-Xorg.x86_64

Instalando xorg-x11-xauth.::

	# yum -y install xorg-x11-xauth

**Archivos de configuración**

En el server debe tener estas lineas /etc/ssh/sshd_config::

	X11Forwarding yes
	X11DisplayOffset 10
	X11UseLocalhost no

Lo cambiamos::

	# sed -i -e 's/\#X11DisplayOffset/X11DisplayOffset/g' /etc/ssh/sshd_config
	# sed -i -e 's/\#X11UseLocalhost\ yes/X11UseLocalhost\ no/g' /etc/ssh/sshd_config

En el cliente debe tener estas lineas ~/.ssh/config (Opcional)::

	Host *
	  ForwardAgent yes
	  ForwardX11 yes

**Test ssh forward a las X**

Nos conectamos al servidor con ssh y le pasamos el parámetro ".X" y debemos consultar la variable DISPLAY y el ssh debe fijarle el valor automáticamente.::
 
	$ ssh -X root@192.168.1.100
	root@192.168.1.100's password: 
	Last login: Wed Oct  3 19:42:07 2018 from 192.168.1.4
	/usr/bin/xauth:  file /root/.Xauthority does not exist
	# echo $DISPLAY
	localhost:10.0

**Instalar unas aplicaciones X** Instalamos el paquete que descubrimos que tiene xclock.::

	# yum -y install xorg-x11-apps-7.7-7.el7.x86_64

**Certificación** Ahora desde el servidor ejecutamos el xclock y debemos ver este aplicativo en nuestras X.::

	# xclock


**Configurado el locale** en ingles para que no pida el paquete adicional de idiomas, se debe levantar la todas las instalaciones con esta configuración.::

	# export LANG=en_US.utf8 LC_ALL=en_US.utf8

	# locale
	LANG=en_US.utf8
	LC_CTYPE="en_US.utf8"
	LC_NUMERIC="en_US.utf8"
	LC_TIME="en_US.utf8"
	LC_COLLATE="en_US.utf8"
	LC_MONETARY="en_US.utf8"
	LC_MESSAGES="en_US.utf8"
	LC_PAPER="en_US.utf8"
	LC_NAME="en_US.utf8"
	LC_ADDRESS="en_US.utf8"
	LC_TELEPHONE="en_US.utf8"
	LC_MEASUREMENT="en_US.utf8"
	LC_IDENTIFICATION="en_US.utf8"
	LC_ALL=en_US.utf8

Lo anterior preferiblemente editamos el /etc/profile y en la ultima linea agregamos el export LANG=en_US.utf8 LC_ALL=en_US.utf8

**Instaladores requeridos para el laboratorio**. Vamos a copiar en el /root todos los paquetes que necesitamos instalar en este laboratorio utilice la técnica que más le guste.

	IDR11.3_CDC_FOR_ACCESS_SVR_LX.zip - Access Server for Linux

	IIDRCDC_10.2.1_DB2_Lnx_x86.zip	- CDC Agent DB2 for Linux

	IIDRCDC_10.2.1_Orcl_Redo_Lnx_x86.zip - CDC Agent Oracle for Linux

	db2_v101_linuxx64_expc_lite.tar.gz - IBM DB2 10.1 for Linux

	oracle-xe-11.2.0-1.0.x86_64.rpm.zip - Oracle XE 11g for Linux










