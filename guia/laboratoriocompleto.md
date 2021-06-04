En este laboratorio tendra dos (2) maquinas virtuales. 
Una maquina virtual con Windows 10 para instalar ahí el Management Console de CDC.
Una maquina virtual con CentOS 7 como Sistema Operativo con 2Gb de RAM y 40Gb de HDD, un (1) Adaptador tipo Bridge, que tendra dos (2) manejadores de Base de datos y sus agentes de CDC correspondientes al manejador de Base de datos y tambien estara ahí el Access Server de CDC.
Los dos (2) manejadores de Base de Datos serán:
	IBM DB2 Express 10.1
	Oracle XE 11g
Los componentes de CDC seran:
	Access Server 11.3.0
	Replication engine for DB2 Linux 10.2.1 (Agent CDC)
	Replication engine for Oracle Linux 10.2.1 (Agent CDC)

* [Configurar CentOS 7](centos7configurarlo.rst) 
* [Instalar DB2-Express 10.1](https://github.com/cgomeznt/DB2/blob/master/guia/instalardb2101.rst) 
* [Instalar Oracle XE 11.1](centos7configurarlo.rst) 
* [Instalar Access Server 11.3.0](accessserver.rst) 
* [Instalar Replication engine for DB2 Linux 10.2.1](agentedb2.rst)
* [Instalar Replication engine for Oracle Linux 10.2.1](agenteoracle.rst)

