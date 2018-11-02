# Conceptos básicos de GNU/Linux

## FileSystem - Sistema de archivos

Es una estructura para ver, encontrar y utilizar ficheros, por otro lado el sistema de archivos abarca todos los archivos separados en esa estructura y sus formatos.

Sistema de archivos | Sistema Operativo | Descripción
------------ | ------------- | ---------------
FAT | Heredado | Este sistema fue adoptado universalmente. Se incluyó en 12 <b>FAT12</b>, 16 <b>FAT16</b> y 32 <b>FAT32</b>.
NTFS | Windows | Este sistema de archivos reemplazó a FAT en sistemas Windows. Todavía es necesario leer las particiones de Windows.
Ext2 | Linux | Segundo filesystem extendido, utilizado por muchas distribuciones Linux
Ext3 | Linux | Tercer filesystem extendido, es la opción predeterminada para Ubuntu. <b>Se agregó journaling</b>.
Ext4 | Linux | Cuarto filesystem extendido, usado en muchas distribuciones Linux. <b>Amplía los límites de almacenamiento</b>.
JFS | Linux | El sistema de archivos de journaling, introducido por IBM y compatible, pero sustituído por Ext4.
XFS | Linux/Irix | Opción de 64 bits más compatible, como una opción en Red Hat.
ReiserFS | Linux/SUSE | Era un formato de archivo que se usaba en varias distribuciones, pero en gran parte se ha sustituído por Ext3.

## Tipos de archivo en LINUX

<b>* Archivos regulares.</b> Contienen datos: archivos de texto, ejecutables o programas, entrada y salida de un programa y similares.
<b>* Directorios.</b> Son archivos/carpetas que corresponden a listas de otros archivos.
<b>* Archivos especiales.</b> Este es el mecanismo utilizado para la entrada y la salida. La mayoría de los archivos de este tipo estan en /dev
<b>* Vínculo.</b> Se trata de un sistema para hacer visible un archivo o directorio en varias partes del árbol de archivos del sistema.
<b>* Sockets de dominio.</b> Tipo de archivo especial que es similar a los sockets TCP/IP en Windows. Proporciona redes entre procesos protegidas por el control de acceso del sistema de archivos.
<b>* Tuberías nombradas.</b> Actúan similar a los sockets y son una manera para que los procesos se comuniquen entre sí, sin utilizar protocolos de socket de red.

<b>Estructura de archivos.</b> Esta estructura es que su <b>/</b> partición, debe ser primaria, mientras que cada otra partición, <b>ya sea primaria o lógica</b> debe montarse a esa partición. Cada partición tendrá un formato de archivo que se configurará y un propósito dentro del SO. Los directorios y archivos se pueden buscar y utilizar dentro de esta estructura.

## Particiones

Es distinto a la forma en conocemos una partición Windows. En Windows, las particiones son de dos tipos: <b>primario</b> y <b>lógico</b>. En un disco SATA IDE más antiguo, estará limitado a 4 particiones primarias o una combinación de varias particiones primarias y lógicas. Cada uno recibe una letra de unidad, pero podrá instalar el sistema en una partición primaria. Actualmente existen tablas GUID/GTP en lugar de MBR que permiten mayores tamaños de disco duro.

En Linux, las particiones también pueden ser <b>primarias</b> y <b>lógicas</b>. Sigue limitado a 4 particiones primarias o una combinación de particiones. Sin embargo, cuenta con las siguientes característiacas:

* Su primera partición será siempre la partición de instalación en una partición primaria.
* Ésta partición a veces se llamará la <b>raíz de la partición</b> o se mostrará como <b>/</b> y, será la partición más importante.
* Se pueden crear más particiones y darles tamaño, formato y propósito, pero normalmente se montarán en el <b>/</b> de esta partición para que realmente funcionen.

## Identificar particiones

A continuación, una tabla comparativa entre particiones Windows y Linux, así como la forma de identificarlas.

Windows


 HD                         | Partición Windows | Identificador Windows  
----------------------------|-------------------|-----------------------
 Primer HD IDE, SCSI, SATA  |  Primera partición| C:                    
 Primer HD IDE, SCSI, SATA  | Segunda partición | D:                    
 Segundo HD, IDE, SCSI, SATA| Primera partición | E:                    
 Segundo HD IDE, SCSI, SATA | Segunda partición | F:                    


Linux


| HD                         | Partición Linux   | Identificador Linux   |
|----------------------------|-------------------|-----------------------|
| Primer HD IDE    (hda)     | Primera partición | hda1                  |
| Primer HD IDE    (hda)     | Segunda partición | hda2                  |
| Primer HD IDE    (hda)     | Primera partición lógica de una extendida 1er disco IDE | hda5       |
| Segundo HD IDE   (hdb)     | Primera partición | hdb1                |
| Segundo HD IDE   (hdb)     | Segunda partición | hdb2                |
| Segundo HD IDE   (hdb)     | Primera partición lógica de una extendida 2do disco IDE | hdb5          |                     
| HD SCSI o SATA   (sda)     | Primera partición | sda1                |
| HD SCSI o SATA   (sda)     | Segunda partición | sda2                | 
| HD SCSI o SATA   (sda)     | Primera partición lógica del 1er disco SCSI | sda5        |
| SCSI             (sdb)     | Segundo disco SCSI/ primera, segunda, lógica| sdb1, sdb2, sdb5        |

Para la instalación de Linux, ya sea de la distribución que sea, se necesita como mínimo dos particiones: la principal, donde se instalará el sistema operativo, formateada con el sistema de archivos que permita la distribución que vayamos a instalar y otra partición llamada swap (intercambio de memoria virtual), esta partición es utilizada como memoria RAM virtual cuando tenemos muchas aplicaciones abiertas y la memoria RAM de nuestro ordenador es insuficiente, de tamaño del swap se suele poner el doble de la memoria RAM, es decir, si tenemos 250 Mb de memoria RAM el tamaño del swap debería de ser aproximadamente de 500 MB, pero estas cifras están pensadas para equipos con poca memoria. Por ejemplo, si te has comprado un equipo nuevo con 4GB de memoria RAM, no es obligatorio que ponga 8GB para el swap. También hay que considerar que si instalas Linux en un equipo con poca memoria y haces mucho uso del swap, tu ordenador se volverá más lento ya que se tarda más tiempo en leer y escribir del disco duro que de la memoria física RAM, en este caso deberías reconsiderar el ampliar la memoria RAM de tu ordenador. 

## Árbol de directorios

En Linux, todo es un fichero, para ello existen directorios que nos referencían la clase de fichero que es. La mayoría de los sistemas Unix/Linux tienen una distribución de archivos estándar, de forma que los recursos y archivos puedan ser fácilmente localizados. Esta distribución forma el árbol de directorios, el cual comienza en el directorio “/”, también conocido como “raíz” o “root”.

No debemos confundir el directorio “root” o “raíz” con el usuario “root” que es el administrador del sistema, ni con el directorio “home” de éste último, ubicado en “/root”. 

Directamente por debajo (dentro) de / hay algunos subdirectorios importantes: /bin, /etc, /dev y /usr, entre otros. Estos a su vez contienen otros directorios con archivos de configuración del sistema, programas, etc.
En particular, cada usuario tiene un directorio “home”. Este es el directorio en el que el usuario guardará sus archivos.

La siguiente figura muestra un árbol de directorio de ejemplo.

```

/ ___ bin
|____ dev
|____ etc
|____ home ___ carlos
|        |____ diego ___ Mail 
|                  |____ articulos ___ notas
|                  |____ cartas
|____ lib
|____ proc
|____ tmp
|____ usr ___ X11R6
        |____ bin
        |____ lib
        |____ local ___ bin
        |         |____ etc
        |____ man
        |____ src ___ linux
        |____ tmp 
```

URL Fuente:

https://smaldone.com.ar/documentos/misdocs/tutorial-gnu-linux/index-3.html
https://www.dell.com/support/article/mx/es/mxbsdt1/sln152018/explicaci%C3%B3n-sobre-los-tipos-y-definiciones-de-particiones-y-directorios-de-ubuntu-linux?lang=es
http://www.aquihayapuntes.com/particiones-y-sistemas-de-archivos-en-linux.html
