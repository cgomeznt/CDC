Instalar Replication engine for Oracle Linux 
=========================================

Descargar el Replication engine for Oracle Linux que se requiera en este caso sera el 11.3, part number CIU0TML

http://www-01.ibm.com/support/docview.wss?uid=swg24038293

Prerequisitos.::

	# yum -y install glibc compat-libstdc++-33

Se requiere las librerias de runtime de i686 para el CDC, Con el instalador de CDC 11.3.3 ya corrigen este detalle.::

	# instalar=`yum search X11 | grep i686 | grep runtime | awk -F":" '{print $1}'`		
	
	# echo $instalar libICE.i686 libICE.x86_64 libSM.i686 libSM.x86_64 libXScrnSaver.i686 libXScrnSaver.x86_64 libXext.i686 libXext.x86_64 libXfont.i686 libXfont.x86_64 libXft.i686 libXft.x86_64 libXi.i686 libXi.x86_64 libXinerama.i686 libXinerama.x86_64 libXmu.i686 libXmu.x86_64 libXp.i686 libXp.x86_64 libXpm.i686 libXpm.x86_64 libXrandr.i686 libXrandr.x86_64 libXrender.i686 libXrender.x86_64 libXt.i686 libXt.x86_64 libXtst.i686 libXtst.x86_64 libXv.i686 libXv.x86_64 libXvMC.i686 libXvMC.x86_64 libXxf86dga.i686 libXxf86dga.x86_64 libXxf86misc.i686 libXxf86misc.x86_64 libXxf86vm.i686 libXxf86vm.x86_64 libdmx.i686 libdmx.x86_64 libfontenc.i686 libfontenc.x86_64 libxkbfile.i686 libxkbfile.x86_64

	# yum -y install $instalar


Descomprimir el paquete.::

	# unzip IIDRCDC_10.2.1_Orcl_Redo_Lnx_x86.zip

Verificamos el instalador y le otorgamos permisos de ejecución.::

	# ls -l
	total 186236
	drwxr-xr-x. 2 root     root          4096 nov  8  2013 IIDR_1021_Oracle
	-rw-r-----. 1 root     root     190669049 sep 26 19:13 IIDRCDC_10.2.1_Orcl_Redo_Lnx_x86.zip

	# cd IIDR_1021_Oracle/

	# ls -l
	total 189480
	-rw-r--r--. 1 root root     22769 Nov  8  2013 InfoSphereDataReplication_Release_Notes_1021_CDC_OracleDatabases.html
	-rw-r--r--. 1 root root 194002134 Nov  8  2013 setup-cdc-linux-x86-oracleredo.bin


	# chmod +x setup-cdc-linux-x86-oracleredo.bin

Procedemos a instalar.::

	# ./setup-cdc-linux-x86-oracleredo.bin

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
	Change Data Capture (Oracle) 10.2

	Respond to each prompt to proceed to the next step in the installation.  If you
	want to change something on a previous step, type 'back'.

	You may cancel this installation at any time by typing 'quit'.

	PRESS <ENTER> TO CONTINUE: 

	===============================================================================


	    International Program License Agreement
	    
	    Part 1 - General Terms
	    
	    BY DOWNLOADING, INSTALLING, COPYING, ACCESSING, CLICKING ON AN
	    "ACCEPT" BUTTON, OR OTHERWISE USING THE PROGRAM, LICENSEE AGREES TO
	    THE TERMS OF THIS AGREEMENT. IF YOU ARE ACCEPTING THESE TERMS ON
	    BEHALF OF LICENSEE, YOU REPRESENT AND WARRANT THAT YOU HAVE FULL
	    AUTHORITY TO BIND LICENSEE TO THESE TERMS. IF YOU DO NOT AGREE TO
	    THESE TERMS,
	    
	    * DO NOT DOWNLOAD, INSTALL, COPY, ACCESS, CLICK ON AN "ACCEPT" BUTTON,
	    OR USE THE PROGRAM; AND
	    
	    * PROMPTLY RETURN THE UNUSED MEDIA, DOCUMENTATION, AND PROOF OF
	    ENTITLEMENT TO THE PARTY FROM WHOM IT WAS OBTAINED FOR A REFUND OF THE
	    AMOUNT PAID. IF THE PROGRAM WAS DOWNLOADED, DESTROY ALL COPIES OF THE
	    PROGRAM.
	    
	 
	Press Enter to continue viewing the license agreement, or enter "1" to 
	   accept the agreement, "2" to decline it, "3" to print it, or "99" to go back
	   to the previous screen.: 1


	===============================================================================
	Choose Install Folder
	---------------------

	Where would you like to install?

	  Default Install Folder: /opt/IBM/InfoSphereChangeDataCapture/ReplicationEngineforOracle

	ENTER AN ABSOLUTE PATH, OR PRESS <ENTER> TO ACCEPT THE DEFAULT
	      : /opt/TS_agent_oracle

	INSTALL FOLDER IS: /opt/TS_agent_oracle
	   IS THIS CORRECT? (Y/N): Y



	===============================================================================
	Pre-Installation Summary
	------------------------

	Please Review the Following Before Continuing:

	Product Name:
	    IBM InfoSphere Change Data Capture (Oracle)

	Install Folder:
	    /opt/TS_agent_oracle

	Link Folder:
	    /tmp/install.dir.12422/Do_Not_Install

	Disk Space Information (for Installation Target): 
	    Required:  388,506,470 Bytes
	    Available: 11,064,111,104 Bytes

	PRESS <ENTER> TO CONTINUE: 


	===============================================================================
	Installing...
	-------------

	 [==================|==================|==================|==================]
	 [------------------|------------------|------------------|------------------]



	===============================================================================
	Install Complete
	----------------

	Congratulations. IBM InfoSphere Change Data Capture (Oracle) has been successfully installed to:
	   /opt/TS_agent_oracle

	You can launch the Configuration Tool at any time by running
	   /opt/TS_agent_oracle/bin/dmconfigurets

	Launch Configuration Tool? (1=Yes, 2=No) (DEFAULT: 1): 2


Cambiamos el propietario de la carpeta para que funcione el usuario replica::

	# chown -R replica. /opt/TS_agent_oracle
	# su - replica

Ahora si podemos ejecutar la herramienta de configuracion .::

	$ /opt/TS_agent_oracle/bin/dmconfigurets

Empieza el proceso de interacción con la configuración::

	Welcome to the configuration tool for IBM InfoSphere Change Data Capture (Oracle). Use this tool to create instances of IBM InfoSphere Change Data Capture (Oracle).

	Press ENTER to continue...


		Press ENTER to continue...

	============================================

	CONFIGURATION TOOL - CREATING A NEW INSTANCE
	--------------------------------------------

	Enter the name of the new instance: agent_oracle
	Enter the server port number [11001]: 11005
	Enter the auto-discovery port number or type 'DISABLE' [DISABLE]: 

	Staging Store Disk Quota is used to limit the disk space used by IBM InfoSphere Change Data Capture staging Store. If this space is exhausted, this instance may run at a lower speed. The minimum value allowed is 1 GB. 

	Enter the Staging Store Disk Quota for this instance (GB) [100]: 1
	Enter the Maximum Memory Allowed for this instance (MB) [1024]: 256
	Enter the bit version (32/64) [64]: 
	Use read-only connection to database (y/n) [n]: 
	Use archive-only mode (y/n) [n]: 
	Select y to use JMS or TCP/IP engine communication connection, select n to use TCP only engine communication connection (y/n) [n]: 
	Enter the path for ORACLE_HOME: /u01/app/oracle/product/11.2.0/xe
	TNS Name:

	1. XE
	2. EXTPROC_CONNECTION_DATA
	3. Other...

	Select a TNS Name: 1
	Would you like to configure advanced parameters (y/n) [n]: 
	Enter the username: system
	Enter the password:
	Retrieving schema list...
	Metadata schema:

	1. ANONYMOUS
	2. APEX_040000
	3. APEX_PUBLIC_USER
	4. APPS-SCHEMA
	5. CTXSYS
	6. FLOWS_FILES
	7. HR
	8. MDSYS
	9. OUTLN
	10. SYS
	11. SYSTEM
	12. XDB
	13. XS$NULL

	Select a database schema for metadata tables: 4

	============================================

	NEW INSTANCE: agent_oracle >> Configuration mode
	------------------------------------------------

	1. Local log reading
	2. Remote log reading
	3. Manual log shipping
	4. Log shipping with Data Guard

	Enter your selection: 1

	Validating database support. Please wait...
	Retrieving ASM info. Please wait...


	Creating a new instance. Please wait...


	Supplemental logging is not turned on for the database.  This is required for IBM InfoSphere Change Data Capture to run successfully
	IBM InfoSphere Change Data Capture will not be able to serve as a source.

	Instance agent_oracle was successfully created.

	Would you like to START instance agent_oracle now (y/n)?n

	============================================

	MAIN MENU
	---------

	1. List Current Instances
	2. Add an Instance
	3. Edit an Instance
	4. Delete an Instance

	5. Exit

	Enter your selection: 5

	Exiting...



Iniciar el agente creado para Oracle::

	$ /opt/TS_agent_oracle/bin/dmts64 -I agent_oracle &

Verificamos el Proceso.::

	$ ps -ef | grep TS_agent_oracle
	replica   18151  17689 44 18:10 pts/2    00:00:07 /opt/TS_agent_oracle/jre64/jre/bin/dmts64-java -cp lib:lib/ts.jar:lib/activation.jar:lib/mail.jar:lib/pbembedded.jar:lib/pbclient.jar:lib/pbtools.jar:lib/cpci.jar:lib/api.jar:lib/commons-cli.jar:lib/asm-all-3.1.jar:lib/jlog.jar:lib/CIoracle.jar -Xmx256M -Xms192M -Xmine64M -XX:NewRatio=1 -Xgcpolicy:gencon -Dcom.sun.management.jmxremote -Djava.ext.dirs=lib/user:jre64/jre/lib/ext -Dcom.datamirror.ts.instance=agent_oracle com.datamirror.ts.commandlinetools.script.Startup -I agent_oracle
	replica   18281  17689  0 18:11 pts/2    00:00:00 grep --color=auto TS_agent_oracle



Verificamos que levante el puerto que configuramos::

	$ netstat -natp | grep -w 11005
	tcp6       0      0 :::11005                :::*                    LISTEN      18151/dmts64-java  


Listo ya tenemos el agente de CDC para Oracle operativo...!!!



