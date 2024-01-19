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
