🌍 1. Ports liés au Web
Service Port Protocole Exemple concret 
HTTP 80 TCP Accès interface web d’un switch non sécurisé 
HTTPS 443 TCP Accès à un firewall via interface web sécurisée 
HTTP Proxy 8080 TCP Proxy d’entreprise (Squid, etc.)
📡 2. Ports DNS / DHCP
Service Port Protocole Exemple concret 
DNS 53 UDP/TCP Résolution de noms (AD, Internet) 
DHCP Serveur 67 UDP Le serveur envoie l’offre d’IP 
DHCP Client 68 UDP Le client reçoit l’IP 
DHCP Relay — — Fonctionne via UDP 67/68 mais traverse les VLANs
🔐 3. Ports de sécurité / authentification
Service Port Protocole Exemple concret 
Kerberos 88 TCP/UDP Authentification AD (tickets) 
LDAP 389 TCP/UDP Requêtes annuaire AD 
LDAPS 636 TCP LDAP sécurisé 
RADIUS 1812 UDP Auth Wi-Fi entreprise 
TACACS+ 49 TCP Auth des équipements réseau 
NTP 123 UDP Synchronisation horaire AD
🧱 4. Ports Windows / Active Directory
Service Port Protocole Exemple concret 
SMB / CIFS 445 TCP Accès \serveur\partage 
RPC 135 TCP Communication AD, GPO 
WMI 5985 / 5986 TCP Supervision, scripts PowerShell 
DFS 445 + RPC TCP Réplication SYSVOL
🧩 5. Ports de messagerie
Service Port Protocole Exemple concret 
SMTP 25 TCP Envoi d’e-mails 
SMTP sécurisé 587 TCP Submission authentifiée 
IMAP 143 TCP Lecture en ligne 
IMAPS 993 TCP IMAP sécurisé 
POP3 110 TCP Téléchargement local 
POP3S 995 TCP POP sécurisé
🖥️ 6. Ports d’administration
Service Port Protocole Exemple concret 
SSH 22 TCP Admin Linux / Switch 
Telnet 23 TCP Admin non sécurisée (à éviter) 
RDP 3389 TCP Connexion Bureau à distance 
VNC 5900 TCP Contrôle à distance
📁 7. Ports de transfert de fichiers
Service Port Protocole Exemple concret 
FTP 21 TCP Connexion FTP 
FTP Data 20 TCP Transfert actif 
SFTP 22 TCP Transfert sécurisé via SSH 
FTPS 990 TCP FTP sécurisé
📡 8. Ports de supervision
Service Port Protocole Exemple concret 
SNMP 161 UDP Collecte d’infos (Zabbix, Centreon) 
SNMP Trap 162 UDP Alertes envoyées par les équipements
🎮 9. Ports divers utiles
Service / Port/ Protocole/ Exemple concret 
MySQL /3306/ TCP/ Base de données applicative 
PostgreSQL 5432/ TCP/ Serveur SQL 
MSSQL/ 1433/ TCP/ SQL Server Windows 
ElasticSearch 9200 TCP Logs / SIEM 
VPN IPSec 500 / 4500 UDP Tunnels VPN 
OpenVPN 1194 UDP VPN SSL
🎯 Résumé express (à connaître par cœur)
Voici les 20 ports les plus importants pour un TSSR :
22 SSH
23 Telnet
25 SMTP
53 DNS
67/68 DHCP
80 HTTP
88 Kerberos
110 POP3
123 NTP
135 RPC
143 IMAP
389 LDAP
443 HTTPS
445 SMB
587 SMTP Auth
636 LDAPS
993/995 IMAPS/POP3S
3389 RDP
5900 VNC

