- En OVH ir a Servidores dedicados y seleccionar el servidor que has contratado.
- Luego de seleccionar podremos ver las especificaciones del servidor.
- Revisar Sistema Operativo y darle click en los puntos suspensivos, Instalar /Reinstalar.
- Seleccionar Instalar desde una plantilla OVH
- Seleccionar Lista para Usar Interfaz Grafica
- En el listados de SO seleccionar Proxmox 5 u otra version, que no sea ZFS, el raid ya viene por defect por hardware (depende de lo que contrataste)
- Check en personalizar la configuración de particiones.

- Dependiendo de tu disco duro 
Primary / aca se instalara el sistema operativo asi que hay que darle mas que 20gb por si piensas instalar un par de herramientas, aunque esto solo se usara de loadbalancer pero es mejor colocarle como minim 50gb si se puede. 

LV /var/lib/vz DATA  aca se instalaran los contenedores y se descargaran las ISO aca debes darle por lo menos buen espacio en nuestro caso 2TB

LV /srv/share BACKUP aca se utilizara por si necesitas compartir folderes con los diferentes contenedores. aca pueden ir scripts 2TB

Y siguiente Elegimos nombre del host y creamos una llave cer para poder conectarnos rapidamente
 y esperamos que se instale.


 - Instalamos iptables persistencias para que los cambios que hagamos en el firewall se queden guardados

#nuevo servidor
 apt install iptables-persistent netfilter-persistent
	
	

#antiguo servidor
 iptables -S #para ver las reglas actuales.

 iptables-save > iptables-export #para guardar las reglas actuales.

 scp iptables-export root@ipnuevo:/temp #para enviar las reglas al nuevo servidor.
	
#nuevo servidor

iptables-save > iptables-old.backup #realizamos un backup de las reglas del nuevo servidor por si falla las del nuevo servidor

#cargamos las reglas del antiguo servidor ojo recordar cambiar el puerto de SSH si no estas usando el mismo por defecto es decir diferente a 22 por que si no lo cambias ya no podras ingresar al servidor

 iptables-restore < /temp/iptables-export


netfilter-persistent restart #para guardar en persistencia


- Instalamos gpg2
apt-get install dirmngr --install-recommends
apt install curl gnupg2

apt-get install git-core zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs yarn

curl -sL https://deb.nodesource.com/setup_12.x | bash -


gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB


\curl -sSL https://get.rvm.io | bash -s stable

source /etc/profile.d/rvm.sh

rvm install ruby-2.5.3

rvm 

gem install foreman


 nohup tar -pczvf MyBackup.tar.gz /srv/share  & en background
