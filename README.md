Ce projet implémente une architecture réseau segmentée utilisant Vagrant et VirtualBox. 
Il simule un environnement de production avec un Firewall, un serveur Web en DMZ et une base de données en LAN.

L'infrastructure est divisée en trois machines virtuelles (Ubuntu 20.04)

|VM1-Firewall | Routeur / Filtrage | Public / DMZ / LAN | 192.168.100.1 / 192.168.10.1 |
| VM2-Web | Serveur Node.js | DMZ | 192.168.100.10 |
| VM3-DB | MySQL Database | LAN | 192.168.10.10 |

Fonctionnalités implémentées

Sécurité & Routage (VM1)
DNAT : Redirection du port 80 vers la VM2 pour exposer le site web.
Masquerading : Permet aux machines internes d'accéder à Internet via la VM1.

Serveur Web (VM2)
Reverse Proxy : Nginx redirige le trafic entrant (port 80) vers l'application Node.js (port 3000).

Base de Données (VM3)
Accessible uniquement depuis le segment LAN.

  Prérequis
- VMWare installé.
- Vagrant installé.
- Git installé.

2. Lancer les machines 
# Allez dans chaque dossier et lancez :
cd VM1firewall -->  vagrant up
cd ../VM2web --> vagrant up
cd ../VM3BD --> vagrant up
