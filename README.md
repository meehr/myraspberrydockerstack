Mein Raspberry Projekt

Ziel ist es mit den hier zur Verfügung gestellten Files einen Raspberry PI 4 mit ein paar Containern zu versehen. 

  1. NginX ReverseProxy ( ein Proxy um Anfragen auf Domains intern weiter zu verteilen ) 
  2. Portainer ( Web-GUI zur Verwaltung der Docker Container )
  3. NextCloud ( Deine eigene Cloud Umgebung ) 
  4. Wireguard ( VPN Server )
  .
  .

Als Basis habe ich das Rasbian 64 Bit Server Image genutzt dieses bekommt ihr entweder direkt über den Raspberry Pi Imager zum download oder ihr ladet euch es manuel runter. 

Nach deinem Update ( sudo apt update && sudo apt upgrade -y ) habe ich noch die notwendigen Docker Pakete installiert ( sudo apt install docker docker-compose ).

Um docker als nonroot laufen zu lassen erfordert es noch ein bissel fein Arbeit. 

Folgende Schritte sind auszuführen.

  1. sudo groupadd docker
  2. sudo usermod -aG docker $USER
  3. newgrp
  
Da ich keine Lust hatte mich mit der weiteren Rechteverwaltung rum zuschlagen, wird der Rest der Aktionen im HomeVerzeichnis des $USER durchgeführt.

Checkt das Git Repo im Homeverzeichnis Eures $USER aus und ihr erhaltet 4 Files

Alles was angepasst werden muss ist entweder in den Files kommentiert oder hat den Wert {changeme}

Reihenfolge der Einrichtung:

  1. Nginx Proxy ( docker-compose -f docker-compose_nginx_proxy.yml up -d --build )
  2. Portainer ( docker-compose -f docker-compose_portainer.yml up -d --build ) Ab hier könnt ihr unter der IP Eures Raspi Port 9000 Portainer erreichen. 
  3. Nextcloud / Wireguard prinzip sollte nun klar sein. 

Vergesst nicht eure Daten anzupassen und euch eine Domain zu besorgen die Ihr auf Euren DDNS Anbieter umbiehen könnt. Sowie Euren Router entsprechend einzustellen. 

Ergänzung 1:

Ich habe von regular Docker Container auf Docker Swarm umgestellt. Grund für diese umstellung war das ich Secrets nutzen wollte und so den DUC (DynamicUpdateClient) meines DDNS Anbieters als Service laufen lassen kann. Hier findet ihr das entsprechende Repo [No-IP](https://github.com/meehr/no-ip) ( Thanks to [@aanousakis](https://hub.docker.com/r/aanousakis/no-ip) for your great Work ) 


"Work on Progress"
