Instalar Replication engine for DB2 Linux 
=========================================

Descargar el Access Server que se requiera en este caso sera el 11.3, part number CIU0UML

http://www-01.ibm.com/support/docview.wss?uid=swg24038293

Prerequisitos.::

	# yum -y install glibc compat-libstdc++-33

Se requiere las librerias de runtime de i686 para el CDC, Con el instalador de CDC 11.3.3 ya corrigen este detalle.::

	# instalar=`yum search X11 | grep i686 | grep runtime | awk -F":" '{print $1}'`		
	
	# echo $instalar libICE.i686 libICE.x86_64 libSM.i686 libSM.x86_64 libXScrnSaver.i686 libXScrnSaver.x86_64 libXext.i686 libXext.x86_64 libXfont.i686 libXfont.x86_64 libXft.i686 libXft.x86_64 libXi.i686 libXi.x86_64 libXinerama.i686 libXinerama.x86_64 libXmu.i686 libXmu.x86_64 libXp.i686 libXp.x86_64 libXpm.i686 libXpm.x86_64 libXrandr.i686 libXrandr.x86_64 libXrender.i686 libXrender.x86_64 libXt.i686 libXt.x86_64 libXtst.i686 libXtst.x86_64 libXv.i686 libXv.x86_64 libXvMC.i686 libXvMC.x86_64 libXxf86dga.i686 libXxf86dga.x86_64 libXxf86misc.i686 libXxf86misc.x86_64 libXxf86vm.i686 libXxf86vm.x86_64 libdmx.i686 libdmx.x86_64 libfontenc.i686 libfontenc.x86_64 libxkbfile.i686 libxkbfile.x86_64

	# yum -y install $instalar



Descomprimir el paquete.::

	# unzip IIDRCDC_10.2.1_DB2_Lnx_x86.zip

Verificamos el instalador y le otorgamos permisos de ejecución.::

	# ls -l
	total 186236
	drwxr-xr-x. 2 root     root          4096 nov  8  2013 IIDR_1021_DB2LUW
	-rw-r-----. 1 root     root     190669049 sep 26 19:13 IIDRCDC_10.2.1_DB2_Lnx_x86.zip

	# cd IIDR_1021_DB2LUW/

	]# ls -l
	total 186872
	-rw-r--r--. 1 root root     24305 nov  8  2013 InfoSphereDataReplication_Release_Notes_1021_CDC_DB2LUW.html
	-rw-r--r--. 1 root root 191329196 nov  8  2013 setup-cdc-linux-x86-db2luw.bin

	# chmod +x setup-cdc-linux-x86-db2luw.bin

Procedemos a instalar.::

	# ./setup-cdc-linux-x86-db2luw.bin 
	Preparing to install...
	Extracting the JRE from the installer archive...
	Unpacking the JRE...
	Extracting the installation resources from the installer archive...
	Configuring the installer for this system's environment...

	Launching installer...

	===============================================================================
	Installer                                        (created with InstallAnywhere)
	-------------------------------------------------------------------------------

	Preparing CONSOLE Mode Installation...




	===============================================================================
	Introduction
	------------

	InstallAnywhere will guide you through the installation of IBM InfoSphere 
	Change Data Capture (IBM DB2) 10.2

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
	Choose Install Folder
	---------------------

	Where would you like to install?

	  Default Install Folder: /opt/IBM/InfoSphereChangeDataCapture/ReplicationEngineforIBMDB2

	ENTER AN ABSOLUTE PATH, OR PRESS <ENTER> TO ACCEPT THE DEFAULT
		  : /opt/TS_agent_DB2

	INSTALL FOLDER IS: /opt/TS_agent_DB2
	   IS THIS CORRECT? (Y/N): y

	===============================================================================
	Pre-Installation Summary
	------------------------

	Please Review the Following Before Continuing:

	Product Name:
		IBM InfoSphere Change Data Capture (IBM DB2)

	Install Folder:
		/opt/TS_agent_DB2

	Link Folder:
		/tmp/install.dir.6887/Do_Not_Install

	Disk Space Information (for Installation Target): 
		Required:  384.744.398 Bytes
		Available: 1.459.994.624 Bytes

	PRESS <ENTER> TO CONTINUE: 

	===============================================================================
	Installing...
	-------------

	 [==================|==================|==================|==================]
	 [------------------|------------------|------------------|------------------]



	===============================================================================
	Install Complete
	----------------

	Congratulations. IBM InfoSphere Change Data Capture (IBM DB2) has been successfully installed to:
	   /opt/TS_agent_DB2

	You can launch the Configuration Tool at any time by running
	   /opt/TS_agent_DB2/bin/dmconfigurets

	Launch Configuration Tool? (1=Yes, 2=No) (DEFAULT: 1): 2

Cambiamos el propietario de la carpeta para que funcione el usuario replica::

	# chown -R replica. /opt/TS_agent_DB2
	# su - replica

Ahora si podemos ejecutar la herramienta de configuracion .::

	$ /opt/TS_agent_DB2/bin/dmconfigurets

Empieza el proceso de interacción con la configuración::

	Welcome to the configuration tool for IBM InfoSphere Change Data Capture (IBM DB2). Use this tool to create instances of IBM InfoSphere Change Data Capture (IBM DB2).

	Press ENTER to continue...

	============================================

	CONFIGURATION TOOL - CREATING A NEW INSTANCE
	--------------------------------------------

	Enter the name of the new instance: agent_DB2
	Enter the server port number [10901]: 11003
	Enter the auto-discovery port number or type 'DISABLE' [DISABLE]: 

	Staging Store Disk Quota is used to limit the disk space used by IBM InfoSphere Change Data Capture staging Store. If this space is exhausted, this instance may run at a lower speed. The minimum value allowed is 1 GB. 

	Enter the Staging Store Disk Quota for this instance (GB) [100]: 1
	Enter the Maximum Memory Allowed for this instance (MB) [1024]: 256
	Enter the bit version (32/64) [64]: 
	Select y to use JMS or TCP/IP engine communication connection, select n to use TCP only engine communication connection (y/n) [n]: 
	Select a DB2 Instance

	1. db2iadm1
	2. Other...

	Select a DB2 Instance: 1
	Select a database name

	1. TEST_DB2
	2. Other...

	Select a database name: 1
	Would you like to configure advanced parameters (y/n) [n]: 
	Enter the username [db2iadm1]: 
	Enter the password:Venezuela21
	Retrieving schema list...
	Metadata schema:

	1. NULLID
	2. SQLJ
	3. SYSCAT
	4. SYSFUN
	5. SYSIBM
	6. SYSIBMADM
	7. SYSIBMINTERNAL
	8. SYSIBMTS
	9. SYSPROC
	10. SYSPUBLIC
	11. SYSSTAT
	12. SYSTOOLS
	13. TEST_DB2
	14. Other...

	Select a database schema for metadata tables [TEST_DB2]: 13
	Would you like to specify a refresh loader path (y/n) [y]: 
	Enter the refresh loader path (y/n) [y]:
	Enter the refresh loader path: /opt/TS_agent_DB2


	Creating a new instance. Please wait...


	Load API test failed and returned the following error A SQL exception has occurred. The SQL error code is '3107'. The SQL state is:      . The error message is: 
	SQL3107W  At least one warning message was encountered during LOAD processing.
	.
	IBM InfoSphere Change Data Capture will not be able to serve as a target.

	Instance agent_DB2 was successfully created.

	Would you like to START instance agent_DB2 now (y/n)?n

	===================================================

	MAIN MENU
	---------

	1. List Current Instances
	2. Add an Instance
	3. Edit an Instance
	4. Delete an Instance
	5. Consolidate Instances

	6. Exit

	Enter your selection:6

	Exiting...

Iniciar el agente creado para DB2::

	$ /opt/TS_agent_DB2/bin/dmts64 -I agent_DB2 &

Verificamos el Proceso.::

	$ ps -ef | grep TS_agent_DB2
	replica   12261  10956 14 17:47 pts/2    00:00:06 /opt/TS_agent_DB2/jre64/jre/bin/dmts64-java -cp /opt/ibm/db2/V10.1/java/db2java.zip:/opt/ibm/db2/V10.1/java/db2jcc4.jar:/opt/ibm/db2/V10.1/java/db2jcc.jar:/opt/ibm/db2/V10.1/java/db2jcc_license_cisuz.jar:/opt/ibm/db2/V10.1/java/db2jcc_license_cu.jar:/opt/ibm/db2/V10.1/bin:/opt/ibm/db2/V10.1/java/common.jar:/opt/ibm/db2/V10.1/java/sqlj.zip:/opt/ibm/db2/V10.1/function:lib:lib/ts.jar:lib/activation.jar:lib/mail.jar:lib/pbembedded.jar:lib/pbclient.jar:lib/pbtools.jar:lib/cpci.jar:lib/api.jar:lib/commons-cli.jar:lib/asm-all-3.1.jar:lib/jlog.jar -Xmx256M -Xms192M -Xmine64M -XX:NewRatio=1 -Xgcpolicy:gencon -Dcom.sun.management.jmxremote -Djava.ext.dirs=lib/user:jre64/jre/lib/ext -Dcom.datamirror.ts.instance=agent_DB2 com.datamirror.ts.commandlinetools.script.Startup -I agent_DB2
	replica   12337  10956  0 17:48 pts/2    00:00:00 grep --color=auto TS_agent_DB2


Verificamos que levante el puerto que configuramos::

	$ netstat -natp | grep -w 11003
	tcp6       0      0 :::11003                :::*                    LISTEN      12261/dmts64-java 


Listo ya tenemos el agente de CDC para DB2 operativo...!!!



