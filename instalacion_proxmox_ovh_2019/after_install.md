- nos conectamos mediante SSH a nuestro servidor mediante la IP

ssh root@ip

- una vez logeado, cambiamos password del root para poder conectarnos a proxmox passwd

- comprobamos proxmox usando la siguiente url https://ip:8006 nos dira que el certificado no es seguro lo aceptamos y colocamos el acceso 

- Añadimos un directorio para los backups

DataCenter > Storage  Add 
Folder /var/lib/vz/dump
Content Archivo VZDump backup

Respaldos Max 2


- cambiamos el puerto para ssh en 
vim /etc/ssh/sshd_config

Cambiamos Port 22 por alguno mas alto.

systemctl restart ssh.service y reiniciamos. probamos conectarnos desde otra pantalla.


- Comentamos los siguientes archivos
/etc/apt/sources.list.d/pve-enterprise.list

y

/etc/apt/sources.list.d/pve-install-repo.list

realizamos un backup de sources.list

cp /etc/apt/sources.list /etc/apt/sources.list.backup

y copiamos el archivo de archivos_necesarios/sources.list a /etc/apt/sources.list


y luego actualizamos el listado

apt update

y luego actualizamos los paquetes

apt dist-upgrade 


- Instalamos fail2ban para protección
apt install fail2ban

- Instalamos nginx para el loadbalancer
apt install nginx
