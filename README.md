# INSTALLATION ET CONFIGURATION DNS
## Table des matières
1. [Installation](#install)
2. [Configuration](#config)
3. [Vérification d'erreurs](#verif)
4. [Création de point d'accès](#wifi)
5. [Test](#test)


### <a name="install"> Installation</a>
` apt-get install dnsutils `  
`apt-get install bind9 `

Quelques explications:

`$TTL` : si on traduit, c’est la durée de vie, autrement dit le temps max que les informations peuvent rester en cache (ici 3600s = 1h)  
`@` : ça fait référence au domaine de base que l’on est en train d’écrire (ici tutorielvideo.fr)  
`IN` : c’est la classe, on le retrouve sur chaque ligne et sur internet c’est la seule option possible (autrement dit, on met toujours IN)  
`SOA` : cet enregistrement sert à indiquer le serveur de nom primaire, l’adresse email à contacter en cas de soucis (le @ remplacer par un .) et des paramètres d’expiration  
`SERIAL` : c’est une sorte de timestamp sous le format “yyyymmddnn”, à changer à chaque modification du fichier pour indiquer une mise à jour  
`Refresh` : indique au bout de combien de temps les serveurs esclaves doivent rafraîchir leurs caches  
`Retry` : délai en seconde que les serveurs doivent attendre avant de faire une deuxième requête si la première a échoué  
`Expire `: le délai en seconde au terme du quel la zone est considérée comme expiré si les serveurs esclaves n’arrivent pas à contacter le serveur primaire  
`Negative cache` : durée de vie minimale de chaque enregistrement présenté plus bas dans le fichier  

### <a name="config"> Configuration</a>
Pour plus de facilité, rendons-nous dans __/etc/bind__ avec la commande `cd /etc/bind/`

* `nano named.conf.local`  
![named.conf.local](/assets/named.conf.local.png)

* `nano named.conf.options`  
![named.conf.options](/assets/named.conf.options.png)

* >`cp /etc/bind/db.local /etc/bind/db.abdoul.mg`   
`cp /etc/bind/db.127 /etc/bind/db.192`

* `nano db.abdoul.mg`  
![db.abdoul.mg](/assets/db.abdoul.mg.png)

* `nano db.abdoul.mg.inv`  
![db.abdoul.mg.inv](/assets/db.abdoul.mg.inv.png)


### <a name="verif"> Vérification d'erreurs</a>
### <a name="wifi"> Création d'un point d'accès</a>
### <a name="test"> Test</a>
