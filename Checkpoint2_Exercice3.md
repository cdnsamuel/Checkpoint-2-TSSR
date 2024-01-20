# Q3.1
Le matériel réseau A est un Switch de niveau 2 (commutateur)
sont rôle est de distribuer les paquets en lisant l'adresse MAC
Dans cette configuration il connecte les appareils d'un même réseau ensemble (10.10.0.0/16)
# Q3.2
Le matériel réseau B est un routeur
Il permet de connecter le réseau 10.10/16 à d'autres réseaux, il est la passerelle de ce réseau
# Q3.3
f0/0 et g1/0 sont les noms des interfaces connectées respectivement aux réseaux 10.10.0.0/16 et 10.12.2.0/24
f pour fast Ethernet 10/100
g pour gigabit Ethernet 10/100/1000
# Q3.4
/16 est le CIDR de ce réseau il indique le nombre de bits allumés pour le masque de sous réseau
c'est l'équivalent du MSR 255.255.0.0
# Q3.5
pour le PC2 10.10.255.254 est une adresse sur un réseau différent du sien qu'il ne peut pas contacter
# Q3.6
| Nom | Adresse réseau | Premiere adresse dispo | Derniere addresse dispo | Broadcast |
| ---- | ---- | ---- | ---- | ---- |
| PC1 | 10.10.0.0/16 | 10.10.0.1 | 10.10.255.254 | 10.10.255.255 |
| PC2 | 10.11.0.0/16 | 10.11.0.1 | 10.11.255.254 | 10.11.255.255 |
| PC5 | 10.10.0.0/15 | 10.10.0.1 | 10.11.255.254 | 10.11.255.255 |
# Q3.7
| Vers\Depuis | PC1 | PC2 | PC3 | PC4 | PC5 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| PC1 | ♾️ | ❌ | ✅ | ✅ | ✅ |
| PC2 | ❌ | ♾️ | ❌ | ❌ | ✅ |
| PC3 | ✅ | ❌ | ♾️ | ✅ | ✅ |
| PC4 | ✅ | ❌ | ✅ | ♾️ | ✅ |
| PC5 | ✅ | ✅ | ✅ | ✅ | ♾️ |
# Q3.8
- PC1
- PC3
- PC4
- PC5
# Q3.9
La perte du premier paquet lors de la mise à jour de la table ARP du switch
# Q3.10
Installer le serveur DHCP sur le PC5 qui est capable de communiquer avec tous les autres
# Q3.11
L'adresse mac de l'émetteur du paquet 5 est 00:50:79:66:68:00
C'est donc la machine qui possède l'ip 10.10.4.2
Il s'agit donc d'une écoute de la carte réseau du PC4
# Q3.12 - Q3.13
La communication capturée est un ping réussi entre

| machine | type | nom | ip | mac |
| ---- | ---- | ---- | ---- | ---- |
| initiateur | request | PC4 | 10.10.4.2 | 00:50:79:66:68:00 |
| cible | reply | PC1 | 10.10.4.1 | - |
| switch |  |  |  | 00:50:79:66:68:03 |
# Q3.14
Le protocole encapsulé dans le paquet 2 est ARP
c'est un protocole de résolution d'adresse utilisé pour faire des traductions MAC <-> IP
(couche 2 <-> couche 3)
# Q3.15
- Matériel A -> Switch : Observé lors de l'utilisation d'ARP, transmet les paquets entre PC1 et PC4
- Matériel B -> Routeur : pas d'intervention dans la capture
# Q3.16
Dans cette trame c'est le PC3 10.10.80.3 qui essaye de joindre une autre machine
# Q3.17
le protocole encapsulé est ICMP, il permet de faire circuler des informations de connectivité et le statut du réseau
# Q3.18 - 3.19
- le PC3 10.10.80.3/16 essaye de communiquer avec le PC2 10.11.80.2/16
- Ils ne sont pas sur le même réseau 
- PC3 remonte donc par sa passerelle, le Matériel B 10.10.255.254 /16
- Matériel B n'est pas sur le même réseau que PC2
- le Matériel B répond donc au PC3 qu'il ne peut pas joindre l'hôte
# Q3.20
- Matériel A -> Switch fait suivre les paquets entre la PC3 et la passerelle
- Matériel B -> Routeur utilisé comme passerelle pour joindre un réseau différent de 10.10.0.0/16, communique avec le PC3
# Q3.21
| type | nom | ip |
| ---- | ---- | ---- |
| source | PC4 | 10.10.4.2 |
| destination | Une machine du nuage | 172.16.5.253 |
# Q3.22 - Q3.23
- MAC Source : ca:01:da:d2:00:1c
- MAC Destination : ca:03:9e:ef:00:38

Déduction :
1. le MAC source n'est pas celui du PC4
2. ca:01:da:d2:00:08 est le MAC f0/0 du matériel B

la communication à donc été enregistrée entre 
- g1/0 du matériel B
- g2/0 du matériel R2
