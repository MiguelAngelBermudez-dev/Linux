## Proceso de arranque (boot process)

Es el procedimiento para encender linux, es todo lo que pasa desde que se ejecuta linux asta que la interfaz esta operativa.

- Imagen proceso de arranque 
	- [[1.png]]
- El roceso de arranque se ejecuta en cadena como vemos en la imagen de arriba y tiene varios rocesos que detallare mas abajo
## bios

Software almacenado en una pequeña memoria volatil del el harware del pc

este es el encargado de inicializar el harware las entradas y las salidas del pc

Este proceso se denomina POST (**P**ower **O**n **S**elf **T**est)

Tambien se encarga de contorlar el proceso de arranque

## **Registro de arranque maestro (MBR) y gestor de arranque**

Una vez terminado el POST pasa a controlar el sistema el boot loader que es el gestor de arranque que se almacena en uno de los discos duros ya sea en el sector de arranque MBR o en el UEFI/EFI para los mas modernos

### gestores de arranques:

El gestor de arranque es el responsable de cargar la imagen del kernel, el disco ram inicial o sistemas de archivos en la memoria

- GRUB (**GR**and **U**nified **B**oot loader)
- ISOLINUX para arranque desde medios extraibles
- DAS U-BOOT para arranques desde dispositivos integrados
Tipos de arranques
	[[2.png]]
## cargador de arranque en accion

El boot loader tiene dos etapas distintas de arranque

### Para sistemas de arranque bios/MBR

El sistema de arranque reside en el primer sector del disco duro

**M**aster **B**oot **R**ecord (**MBR**)

En esta etapa el gestor de arranque examina la tabla de particiones

y encuentra una particion de arranque

Una vez que la encuentra busca la segunda etapa

GRUB y la carga en la memoria ram

### Para sistemas de arranque EFI/UEFI

El firware de la uefi lee los datos del boot manager para ver que aplicacion uefi se va a lanzar y desde donde luego inicializa el firware la aplicaicon GRUB

En la segunda etapa encuentra un /boot que nos permite elegir que sistema operativo arrancar si tubiera mas de uno luego carga el nucleo del sistema operativo seleccionado en la ram y le pasa el control

## Disco RAM inicial

### initramfs

continene programas y archivos binarios que contiene todas las aacciones para montar un sistema de archivos raiz proporciona funcionalidad kernel para los archivos necesarios y controladores.

LOs conbtroladores de alamcenamiento masivos se con una instalacion llamada udev (user divice) que se encarga de averiguar los dispositivos presentes, los controladores de disppositivo averigua donde estan y los carga y una vez que se monta el fichero raiz se comprueba si hay errores y se monta.

### Mount

indica que el sistema de archivos esta listo y lo asocia a un punto del sistema de archivos (el **mount point**)

si tiene exito el initramfs se borra de la ram y carga el programa init (**/sbin/init**)

### Init

Se encarga del montaje del sistema de ficheros raiz

- Imagen disco ram inicial
	- [[3.png]]
## Inicio de secion en modo texto

init inicia varias solicitudes de secion en modo texto esto permite esciber en nombre de usuario, contraseña y la interfaz shell de comandos, si ejecutas una interfaz grafica la shell no aparecera.

normalmente la shell de linea de comandos ppredeterminado es bash

## Kenel de Linux

El gestor de arranque es el encargado de cargar el kernel

y tambien es el encargado de iniciar el iframfs sistema de archivos inicial basado en ram

- imagen de como se gestiona el arranque
	- [[4.png]]
Cunado el kernel se carga en la ram inicializa y configura la memoria del equio y tambien todo el harware conectado al sistema

## **/sbin/init y Servicios**

El kernel se encarga de ejecutar /sbin/init luego este pasa al proceso inicial y se encarga de iniciar otros procesos del sistema a ecepcion de los procesos que se arrancados y gestionados por el propio kernel que se denominan procesos kernel

### Init

Es el responsable de mantener el sistema y apagarlo, actua como gestor de procesos que no sean de kernel, realiza limpieza, reinicia los servicios de inicio de secAion de usuario

### system v

inicio de sistema de forma secuencial por niveles de **runlevels**

### Systemd

Es mas moderno y el que se usa a dia de hoy se ejecuta de forma paralela las funciones

## Alternativas de inicio

- SystemVinit:
    - Ejecuta procesos en series dividido por etapas secuenciales este proceso no a probecha bien el rocesamiento paralelo devido a que necesita que un proceso termine para continuar con el otro
- Systemd:
    - utiliza el procesamiento paralelo lo que permite iniciar servicios en paralelo
    - systemd se hace cargo del proceso init
    - podemos iniciar, detener y reestablecer un sevicio con los comandos: systemctl start, systemctl stop y systemctl restart
    - podemos habilitar o desabilitar un servicio al arrancar nuestro os systemctl enable o systemctl disable (y el nombre del servicio)

## Sistema de fichero de linux

Es un metodo de almacenamiento y organizacion

Hay diferentes tipos de ficheros compatibles con linux

- FIlesystem de discos combencuionales
    - ext3
    - ext4
    - XFS
    - Btrfs
    - Jfs
    - NTFS
    - vfat
    - exfat
- sistema de almacenamiento flash
    - ubifs
    - jffs2
    - yaffs
- Filesystem de base de datos
- Filesystem con fines especiales:
    - procfs
    - sysfs
    - tmfs
    - **squashfs**
    - **debugfs**
    - **fuse**

## Particiones y sistemas de archivos

- **particion:** es una sesccion fisica contigua de un disco
    
- **filesystem**: un metodo para almacenar/buscar archivos en un disco duro
    
- Comparativa entre sistemas de archivos windows y linux
    
    ||**Windows**|**Linux**|
    |---|---|---|
    |Partición|**Disco1**|**/dev/sda1**|
    |Tipo de sistema de archivos|NTFS/VFAT|EXT3/EXT4/XFS/BTRFS...|
    |Parámetros de montaje|Letra de unidad|Punto de montaje|
    |Carpeta base (donde se almacena el SO)|C:\|/|
    

## Estandar de jerarquia de un sistema de archivos

- los sistemas linux almacenan sus archivos siguiendo el estandar FHS(**F**ilesystem **H**ierarchy **S**tandard)
    
- Linux usa / para separar rutas y no tiene letra de unidad
    
- Jerarquia de archivos
	    [[5.png]]
    
    
- Todos los nombres de los directorios distingen entre mayuscula y minuscula or lo que Boot y boot no son el mismo directorio
    

## Eleccion de una distribucion linux

- Distrubuciones linux
	- [[6.png]]
### Preguntas que hacerte a la hora de la eleccion

- ¿Cuál es la función principal del sistema (servidor o escritorio)?
- ¿Qué tipos de paquetes son importantes para la organización? Por ejemplo, servidor web, procesamiento de textos, etc.
- ¿Cuánto espacio en disco duro se necesita y cuánto hay disponible? Por ejemplo, al instalar Linux en un dispositivo integrado, el espacio suele estar limitado.
- ¿Con qué frecuencia se actualizan los paquetes?
- ¿Cuánto dura el ciclo de soporte para cada versión? Por ejemplo, **LTS** las versiones tienen soporte a largo plazo.
- ¿Necesita la personalización del núcleo del proveedor o de un tercero?
- ¿En qué hardware estás ejecutando? Por ejemplo, podría ser **X86**, **ARM**, **PPC**, etc.
- ¿Necesitas estabilidad a largo plazo? ¿Puede aceptar (o necesitar) un sistema de vanguardia más volátil que ejecute el software más reciente?

### planificacion

Es importante hacerlo bien desde el principio por que una vez montado es dificil de modificar

- Particionado de disco
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1d5206a5-6ad0-4473-af90-a63fa660c6f6/5414e674-9bb4-4967-894d-bd46c3f13325/Untitled.png)
    

### Opciones de software

Todos los instaladores rte permiten tener las opciones minimas de software o personalizarlo instalando lo que tu requieras

En cuanto a seguridad todos los usuarios pueden establecer sus contraseñas al principio de la instalacion y en casos mas avanzados liunux segun la distribucion permite sistemas de seguridad como SElinux por RHE o appArmor (ubuntu)

### Funetes de instalacion

- Las distribuciones linux se proporcionan en medios extraibles como usb cd
- ambién admiten arrancar una imagen pequeña y descargar el resto del sistema a través de la red
- los instaladores te permiten completamente hacer una instalacion automatica usando archivos de configuracion especificos ste archivo se denomina archivo Kickstart para sistemas basados en Red Hat, perfil AutoYast para sistemas basados en SUSE y archivo Preseed para sistemas basados en Debian.

### Proceso de instalacion

Primer paso configuras la bios el sistema uefi para que arranque desde la unidad estraible

Segundo paso el sistema operativo te hace una serie de preguntas de configuracion

Por ultimo se reinicia el equipo ya con la imagen instalada

Algunos instaladores te dan la opcion de instalar paquetes de software pero para ello necesitamos conexion a internet

### a tener en cuenta

al realizar una isntalacion en tu disco el dsico se formateara por lo que se perdera todo tipo de informacion en el