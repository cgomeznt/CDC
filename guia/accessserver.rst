IBM InfoSphere Change Data Capture v11.3 Access Server for Linux x86 Multilingual
==================================================================================

Descargar el Access Server que se requiera en este caso sera el 11.3
http://www-01.ibm.com/support/docview.wss?uid=swg24038293


Descomprimir el paquete.::

	# unzip IDR11.3_CDC_FOR_ACCESS_SVR_LX.zip

	# ls -l
	total 230120
	-rw-r--r--. 1 root     root     235610157 sep 26 18:54 IDR11.3_CDC_FOR_ACCESS_SVR_LX.zip
	drwxr-xr-x. 2 root     root          4096 jun  3  2014 IIDR_1130_AccessServer

	# cd IIDR_1130_AccessServer/

Instalamos.::

	# ls -l
	total 231040
	-rw-r--r--. 1 root root 236556494 jun  3  2014 iidraccess-11.3-3236-linux-x86-setup.bin
	-rw-r--r--. 1 root root     20619 jun  3  2014 IIDR_Release_Notes_113_CDC_ManagementConsole.html

	# chmod +x iidraccess-11.3-3236-linux-x86-setup.bin

.::

	# ./iidraccess-11.3-3236-linux-x86-setup.bin 
	Preparing to install...
	Extracting the JRE from the installer archive...
	Unpacking the JRE...
	Extracting the installation resources from the installer archive...
	Configuring the installer for this system's environment...

	Launching installer...

	===============================================================================
	IBM InfoSphere Data Replication Access Server    (created with InstallAnywhere)
	-------------------------------------------------------------------------------

	Preparing CONSOLE Mode Installation...




	===============================================================================
	Introduction
	------------

	InstallAnywhere will guide you through the installation of IBM InfoSphere Data 
	Replication Access Server.

	It is strongly recommended that you quit all programs before continuing with 
	this installation.

	Respond to each prompt to proceed to the next step in the installation.  If you
	want to change something on a previous step, type 'back'.

	You may cancel this installation at any time by typing 'quit'.

	PRESS <ENTER> TO CONTINUE: 

	===============================================================================


	 
	 
		Acuerdo Internacional de Programas bajo Licencia
		
		Parte 1 - Condiciones Generales
		
		EL LICENCIATARIO ACEPTA LOS TÉRMINOS DE ESTE ACUERDO MEDIANTE LA
		DESCARGA, INSTALACIÓN, COPIA, ACCESO, PULSANDO EL BOTÓN "ACEPTAR" O
		MEDIANTE CUALQUIER TIPO DE UTILIZACIÓN DEL PROGRAMA. SI EL CLIENTE
		ACEPTA ESTOS TÉRMINOS EN NOMBRE DEL LICENCIATARIO, EL CLIENTE DECLARA
		Y GARANTIZA QUE TIENE PLENA AUTORIDAD PARA OBLIGAR AL LICENCIATARIO A
		CUMPLIR DICHOS TÉRMINOS. SI EL CLIENTE NO ACEPTA ESTOS TÉRMINOS, NO
		DEBERÁ
		
		* DESCARGAR, INSTALAR, COPIAR, ACCEDER, PULSAR EL BOTÓN "ACEPTAR" NI
		USAR EL PROGRAMA; Y DEBERÁ
		
		* DEVOLVER INMEDIATAMENTE LOS MEDIOS NO UTILIZADOS, LA DOCUMENTACIÓN Y
		EL DOCUMENTO DE TITULARIDAD A LA ENTIDAD A LA CUAL LOS ADQUIRIÓ PARA
		EL REEMBOLSO DEL IMPORTE PAGADO. SI EL PROGRAMA FUE DESCARGADO,
	 
	Pulse Intro para seguir visualizando el acuerdo de licencia, o entre "1" 
	   para aceptar el acuerdo, "2" para no aceptarlo, "3" para imprimirlo, "5" 
	   para visualizarlo en inglés, o "99" para volver a la pantalla anterior.: 1

	===============================================================================


	Enter the TCP/IP port for Access Server.
	P&ort Number: (DEFAULT: 10101): 11010

	===============================================================================
	Choose Install Folder
	---------------------

	Where would you like to install?

	  Default Install Folder: /opt/IBM/InfoSphereDataReplication/AccessServer

	ENTER AN ABSOLUTE PATH, OR PRESS <ENTER> TO ACCEPT THE DEFAULT
		  : /opt/TS_AccessServer

	INSTALL FOLDER IS: /opt/TS_AccessServer
	   IS THIS CORRECT? (Y/N): Y

	===============================================================================
	Configure User Data Folder
	--------------------------

	Access Server requires a folder to store logs, configuration information and 
	user data. Specify a folder where this information should be stored.

	  
	Where would you like your user data folder?

	Default User Data Folder: /opt/TS_AccessServer

	   
	   ENTER AN ABSOLUTE PATH, OR PRESS <ENTER> TO ACCEPT THE DEFAULT: 

	===============================================================================
	Pre-Installation Summary
	------------------------

	Please Review the Following Before Continuing:

	Product Name:
		IBM InfoSphere Data Replication Access Server

	Install Folder:
		/opt/TS_AccessServer

	Link Folder:
		/root

	User Data Folder:
		/opt/TS_AccessServer

	Disk Space Information (for Installation Target): 
		Required:  295.707.455 Bytes
		Available: 2.023.120.896 Bytes

	PRESS <ENTER> TO CONTINUE: 

	===============================================================================
	Installing...
	-------------

	 [==================|==================|==================|==================]
	 [------------------|------------------|------------------|------------------]



	===============================================================================
	Installation Complete
	---------------------

	Congratulations. IBM InfoSphere Data Replication Access Server has been 
	successfully installed to:

	/opt/TS_AccessServer

	Before you connect to this Access Server installation, you must start Access 
	Server and create the administration user account. See the installation guide 
	for more information. You should also install the equivalent version of IBM 
	InfoSphere Data Replication Management Console, if you haven't already done so,
	before connecting to Access Server.


	PRESS <ENTER> TO EXIT THE INSTALLER: 

Creamos un grupo y usuario::

	# groupadd replica
	# useradd -g replica  -m -d /home/replica replica -p password1
	# su - replica

Iniciamos el servicio.::
	
	$ /opt/TS_AccessServer/bin/dmaccessserver &

Verificamos.::

	$ ps -ef | grep TS_
	replica      6299  2804  1 19:08 pts/0    00:00:00 /opt/TS_AccessServer/jre64/jre/bin/dmaccessserver-java -Duser.folder=/opt/TS_AccessServer -server -Xmx512m -jar lib/server.jar 11010
	replica      6328  2804  0 19:09 pts/0    00:00:00 grep -i TS_

	$ netstat -an | grep -w 11010
	tcp        0      0 :::11010                    :::*                        LISTEN


