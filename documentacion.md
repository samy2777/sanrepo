# DOCUMENTACION DEBIAN
## Comandos Basicos
#### Edición
```
en GNU/ Linux este numeral # significa titulo
mas de un  numeral ## significa subtitulo
```
*editor de texto que guarda con extensión md   ejemplo introduccion.md
```
Medit introduccion.md
```
*listar archivos
```
Ls  -l        (para mostrar archivos  -l con detalle)
```
*listar archivos, ordenar por fecha de modificación
```
Ls  -lahtr (  para mostrar archivos  ordenados por fecha de modificación)      `
```
*listar directorios
```
Mkdir  nombre_de_carpeta `
```
*listar sub directorios  (crear subcarpetas)
```
Mkdir  -p /nombre_de_carpeta/subcarpetas 
Mkdir   /temp/xxx/qqq/aaa/aaa/(c1,c2,c3,c4,c5,c6) 
Mkdir ./hola/  (.directorio actual)
Mkdir -/hola/  (.directorio en home)
```
*crear archivo en blanco
```
Touch nombre_archivo
```
*Editar archivos
```
Nano, vi,vim, etc
```
*resultado de un comando almacenado en un archivo
```
Ls –l > nombre_archivo
Ls –l >> nombre_archivo   (ejemplo hola.txt + hola.txt)
Tail .F hola.txt
```
*buscar una palabra aa  dentro un archivo

```
Grep  -n aa  hola.txt
    -n me muestra la línea en la que está la palabra
    -nR es búsqueda recursiva en varios archivos no solo en hola
```
*buscar un archivo
```
Find directorio  -name nombre_archivo
Find   (signo bag estach) name /*la/*
```
*muestra el manual de ciertos comandos
```
Man find 
```
*muestra LA RUTA DEL ARCHIVO
```
Whereis nano
```
*borrar ARCHIVO
```
-rm archivo
```
*como obtener privilegios de administrador
```
Sudo mkdir /opt/aaa
```
*ingresar a carpetas
```
cd documentos
```
*Salir
```
cd..
```
*comandos para instalación de paquetes
```
apt –get install nombre_paquete  C
aptitude install nombre_paquete C
```
*El usuario root y los miembros del grupo sudo son los únicos que tienen permisos para utilizar 
las máquinas virtuales KVM. Por tanto debemos hacer a nuestro usuario miembro del grupo sudo
```
adduser sandra sudo
Apt-get install sudo   /en sandra
ADDUSER SANDRA sudo
GROUPS EN SANDRAM
```
*Comandos Abreviados
```
Ctrol +o (guardar)  
Ctrol +X (cerrar)
Ctrol +K (para copiar)
Ctrol +U (para pegar)
```
*Comando para reiniciar como root (administrador)
```
Reboot 
```
#### Instalación de Linux

```
*1da partición
```
Dejar 2 GB, PRIMARIA de nombre SWAP de tipo (intercambio)
o más todo depende del equipo y su memoria si tienes 8gb en ram 4 es para intercambio en una partición otros indican que es el doble de la memoria  (intercambio)
```
*2ra partición
```
Dejar 15 GB, LOGICA de nombre HOME  de tipo (sistema de archivo ext4)
para  home(elegir en punto de montaje)  Directorio personal de usuarios 
```		
*3ra partición
```
Dejar 45 GB, LOGICA de nombre DATOS de tipo (sistema de archivo ext4) 
o lo que se tenga siempre >10gb se elige manualmente  ejemplo /datos el tamaño mejor, acá se instalaran las maquinas virtuales.
```
*4ta partición
```
Dejar 20 GB, LOGICA de nombre  RAIZ de tipo (sistema de archivo ext4) 
```
Se aceptan todos los cambios
Ya instalados
Esc no es necesario elegir región cuando estamos trabajando con CD
Luego te pide elegir programas (solo instalar la básica) y continuar
```
####Configuración de Red 
*Verificar con estos comandos para instalar las tarjetas de red
*Para instalar mi tarjeta de red
```
aptitude search (modelo de tarjeta )
```
Como dar privilegios de root 
```
Lspci | grep –i network  /o tambien
Lspci | grep –i  eternet
```
*Vamos a modo consola (DOS), ahí escribimos:
```
Gnome-control-center network
```
Nos aparece la ventana de configuración de IP, ahi elegimos IPV4 y colocamos la IP,
mascara de Red, puerta de enlace y el DNS.
*modo consola
```
auto eth0
iface eth0 inet static
address 192.168.10.41
netmask 255.255.255.0
gateway 192.168.10.1
nameservers 200.87.100.10, 200.87.100.40

```
*nota importante
*tambien edita el dns
```
nano /etc/resolv.conf   
comentar todo y solo debe quedar
nameserver 200.87.100.10
nameserver 200.87.100.40

```
###Configuración del sources.list
* Esta configuración es importante para continuar con la instalación de paquetes dentro de Debian (linux)
y debe ser realizada como usuario root
```
nano /etc/apt/sources.list (editar este archivo)
```
```
deb http://192.168.55.62/ftp.us.debian.org/debian 
wheezy main contrib
deb http://192.168.55.62/ftp.br.debian.org/debian 
wheezy main contrib
```
* NOTA: Dentro este archivo sources.list comentar CD, de otro modo al momento de utilizar el apt-get install 
nos eviara a la unidad de CD
*cambiar de usuario
```
su Sandra
```
### Creación de un Repositorio
*CREAR UNA CUENTA EN GITHUB.COM
*CREAR AHÍ MISMO UN REPOSITORIO
Ahora nos vamos al home root
Dentro de proyecto
Git remote add origin https://github.com/sivadmp/documentacion.git
Git add REAME.TXT
GIT config –global user.name “samy”
GIT config –global user.name “samy2_777@hotmail.com”
Git commit
Git push origin master

###Como montar un CD ISO
* Crear primero una carpeta
```
MKDIR /DVD1
```
* Luego montar el iso con sudo
```
Sudo mount /dirección del iso RAIZ
```
###Para cargar un CD
```
/ETC/APT/SOURCES.LIST

```

### Virtualzación completa – kvm
* Nota tambien se puede virtualizar con Virtualización ligera – LXC, Docket
*verificar si nuestra computadora soporta la virtualización con el siguiente comando
INTEL
```
grep vmx/proc/cpuinfo
```
PARA AMD
```
grep svm/proc/cpuinfo
```
*Instalar KVM
```
apt-get install qemu-kvm libvirt-bin virtinst virt-viewer
```
*Instalar el paquete para administrar
```
apt-get install virt-manager
```
*Añadiendo
```
adduser sandra kvm && adduser sandra libvirt
```

Nota:Libvirt: Librería escrita en C (C toolkit) para interactuar con las recientes capacidades de virtualización de las versiones modernas de Linux (y de otros sistemas operativos).
home/sandra# grep vmx  /proc/cpuinfo

*Este comando es para incrementar el sistema de archivos

```
Lvextend –L*100M /dev/mapper/sistemas-tmp
umount /dev/mapper/sistemas-tmp  (este comando es para desmontar )
e2fsck –f  /dev/mapper/sistemas-tmp
resize2fs /dev/mapper/sistemas-tmp
df –h 
```
* Espacio reservado de disco de la virtual
```
Gvs
```
* Este comando muestra el tamaño de la partición
```
lvs 
```
*Caso con Home
```
1. Lvextend –L*100M /dev/mapper/sistemas-home
2. umount /dev/mapper/sistemas-home  
3. e2fsk –f  /dev/mapper/sistemas- home (como commit)
4. mount /tmp
5. df -h
```
*Ahora a Reducir el tamaño  la partición
```
1. Umount /dev/mapper/sistemas-tmp
2. e2fsck –f  /dev/mapper/sistemas-tmp
3. Resize2fs /dev/mapper/sistemas-tmp 100M  (estos 100 M es al que quiero llegar)
4. Mount  /tmp
5. Lvreduce –L 100M /dev/sistemas/home  (aquí te pregunta si realmente quierer quitar el momento)
6. Vgs (ver si se hizo o no)
7. vls
8. df -h
```
###Trabajando en el Gestor de Maquinas Virtuales
*Creando un nuevo disk en la maquina virtual
En HOST Click derecho DETALLES En almacenamiento CREAR un disco   Aux de 2 gb
En la Maquina virtual Click derecho Abrir
Adicionar hardware   adiciionarmos el disco que creamos como Aux como SCI en Disk bus y qcow2 en storage format.
```
Fdisk –l |more
Vgdisplay
pvdisplay  (muestra el volumen físico)
Cfdisk /dev/vdb ( Cfdisk es un editor para particionar discos, cuando hacemos cambios hacemos siempre Write)  
Fdisk –l |more
```
*Aquí creamos vdb1
```
pvcreate /dev/vdb1 (muestra los volúmenes físicos de los discos)
```
luego mostramos con PVdisplay
```
vgcreate GRUPOA  /dev/vdb (aquí creamos el  GRUPO y asignamos el disco)
lvs
lvcreate –L 500m –n volumen01  grupoA  (creamos un nuevo volumen de 500 megas que este dentro del grupo A)
df –h
mkfs.ext3 –m 0 /dev/mapper/grupoA-volumen01
```
le damos un sistema de archivos de tipo ext3 a la partición q hemos creado

*Ahora montamos la partición pero primero creamos una carpeta para montarla ahi
```
Mkdir /mnt/crearcarpeta
Mount /dev/mapper/grupoA-volumen01 /mnt/crearcarpeta
Df –h
Mkdir –p /mnt/volumen-01/datos/   FALTA
Nano /etc/fstab/     (es un fichero de boot de discos )
```
*Aquí cambiamos



###Como instalar un iso
*1.- redimensionar el disco duro virtual
```
Qemu-img resize ruta_disco +5g
```
*2.- Bootear desde el CD-rom (gparted.eso)
192.168.55.100/iso/  bajar este iso
```
Sudo cp(n)/descargas/gparted.iso   
```
*Datoses para colocar lo descargado en descargas en la carpeta datos
```
/datos$ ls gparted.iso  (ver que esta en datos)
```
Apagar máquina virtual

###agregar hardware a la virtual
*hardwareorage cd romm y finalizar  esto para tener un cd si ya lo tenemos no hacer nada)
*Luego ir  a opciones de booteo y hacer que botee primero el cd luego disco duro
Seleccionar la primera opción y luego enter
0 y enter (esto para iniciar de modo grafico)
*Expandir la partición extendida desde el modo gráfico
*Seleccionar la partición extendida 
*redimensionar
*Luego aplicar
*expandir la partición LVM, desde el modo grafico
*Seleccionar la partición lvm 
*redimensionar
*Luego aplicar
```
Fdisk –l /dev/sda  (aquí nos muestra que la partición de este disco a sido redimensionado)
```
*Reiniciar la maquina virtual
   ```
        Reboot
        ```
