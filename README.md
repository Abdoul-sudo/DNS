# INSTALLATION ET CONFIGURATION DNS
## Table des matières
1. [Installation](#install)
2. [Configuration](#config)
3. [Vérification d'erreurs](#verif)
4. [Création de point d'accès](#wifi)
5. [Test](#test)


## <a name="install"> Installation</a>
` apt-get install dnsutils `  
`apt-get install bind9 `

## <a name="config"> Configuration</a>
Pour plus de facilité, rendons-nous dans __/etc/bind__ avec la commande `cd /etc/bind/`  
Ensuite, commençons à configurer les fichiers:

* `nano named.conf.local`  
![named.conf.local](/assets/named.conf.local.png)

>`type master `: indique qu’il s’agit du serveur dédié maitre   
`allow-query` : indiquer qui est-ce qu'on autorise à intérroger le serveur  
`file “/etc/bind/db.abdoul.mg”` : indique le fichier qui contient les informations sur le nom de domaine et les sous domaines.  

* `nano named.conf.options`  
![named.conf.options](/assets/named.conf.options.png)

* `cp /etc/bind/db.local /etc/bind/db.abdoul.mg`   
`cp /etc/bind/db.127 /etc/bind/db.abdoul.mg.inv`

* `nano db.abdoul.mg`  
![db.abdoul.mg](/assets/db.abdoul.mg.png)

* `nano db.abdoul.mg.inv`  
![db.abdoul.mg.inv](/assets/db.abdoul.mg.inv.png)

### Quelques explications:
`$TTL` : c’est la durée de vie (temps maximal de sauvegarde en cache des informations) (ici 604800s)   
`SOA` : cet enregistrement sert à indiquer le serveur de nom primaire, l’adresse email à contacter en cas de soucis (le @ remplacer par un .) et des paramètres d’expiration  
`Refresh` : indique au bout de combien de temps les serveurs esclaves doivent rafraîchir leurs caches  
`Retry` : délai en seconde que les serveurs doivent attendre avant de faire une deuxième requête si la première a échoué  
`Expire `: délai en seconde auquel la zone est considérée comme expiré si les serveurs esclaves n’arrivent pas à contacter le serveur primaire  
`Negative cache` : durée de vie minimale de chaque enregistrement présenté plus bas dans le fichier  
`@` : ça fait référence au domaine de base écrit  
`IN` : c’est la classe, on le retrouve sur chaque ligne et sur internet c’est la seule option possible (autrement dit, on met toujours IN)  
`NS` : sert à définir quels serveurs répondent pour une zone donnée (pointe vers un enregistrement de type A)  
`MX` : sert à définir vers quel serveur de la zone un email à destination du domaine doit être envoyé (pointe vers un enregistrement de type A) 



## <a name="verif"> Vérification d'erreurs</a>
En cas d"erreur, pour vérifier ce que c'est et où elle se trouve, il suffit de lancer la commande:   
 __named-checkconf -z__ et   
__named-checkzone nomdedomaine. db.nomdedomaine__  
![verif.err](/assets/verif.err.png)

## <a name="wifi"> Création d'un point d'accès</a>
* Créer un nouveau réseau wifi  
![wifi1](/assets/wifi1.png)

* Permettre à tout utilisateur de se connecter dessus  
![wifi2](/assets/wifi2.png)

* Mode Ad hoc  
![wifi3](/assets/wifi3.png)

* On ajoute l'adresse du serveur  
![wifi4](/assets/wifi4.png)

## <a name="test"> Test</a>
* Après s'être connecté au point d'accès créé précédement, il faut ajouter dans __/etc/resolv.conf__  :  
`nano /etc/resolv.conf`  
![resolv.conf](/assets/resolv.conf.png)

* Redémarer bind9 avec: `systemctl restart bind9`  
Vérifiez le status `systemctl status bind9`  
![status.bind9](/assets/status.png)

* Tester:  
`ping 192.168.1.1`  
`ping abdoul.mg`
![ping](/assets/ping.png)


