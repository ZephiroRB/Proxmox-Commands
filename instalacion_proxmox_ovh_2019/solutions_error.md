 al cambiar el puerto de SSH o al no quere abrir  asignar

 iptables -I INPUT -p tcp --dport 3899 -j ACCEPT

 cambiando puerto..

 reasignar puertos

 iptables -t nat -A PREROUTING -i vmbr0 -p tcp -m tcp --dport 10090 -j DNAT --to-destination 192.168.0.190:10090


 sysctl fs.inotify.max_user_instances=556 error many connections


Cuando no abre las conecciones internet en los servidores internos

 ip addr flush dev vmbr0

y reiniciar desde el OVH.


grep -irn "/etc/nginx" -e  "dev.contentbreeze"
