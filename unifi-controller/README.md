# Configuration du Contrôleur Unifi avec Traefik via Docker-Compose

## Objectif:
Installer et configurer un contrôleur Unifi, une interface de gestion de réseaux Wi-Fi, avec Traefik comme reverse proxy.

## Prérequis :
Docker-compose installés.  
Nano installé.  
Curl installé.  

## Étape 0: Préparation de l'Environnement de Travail
Créer un dossier pour le docker-compose  

Utilisez
```
mkdir unifi-controller
```

Allez dans le dossier du docker-compose

Utilisez
```
cd unifi-controller
```

## Étape 1: Configuration du Fichier .env pour Portainer
Créer le fichier .env  

Utilisez 
```
nano .env
```
Ajoutez le contenu, en remplaçant "unifi.domaine.tld" par votre domaine FQDN sur la ligne "TREAFIK_FQDN="  
Ajoutez votre mot de passe, en remplaçant "password" par votre mot de passe sur la ligne "DB_PASSWD="  

Pour quitter "nano" faites "CTRL"+"X" ensuite "Y" et "ENTER"  

## Étape 2: Création et Configuration de docker-compose.yml pour Unifi-Controller
Créer et configurer docker-compose.yml pour Unifi-Controller:

Utilisez 
```
nano docker-compose.yml
```
Copier le contenu.

Pour quitter "nano" faites "CTRL"+"X" ensuite "Y" et "ENTER"  

## Étape 3: Configuration du DNS:

Récupérez l'ip publique de la machine afin de faire un enregistrement chez votre fournisseur DNS  

Utilisez 

```
curl ifconfig.net
```

Ensuite allez sur le site de votre hébergeur DNS afin de faire un enregistrement de "type A"

example: trae.domain.tld = [IP PUBLIQUE]


## Étape 4: Lancement de Unifi-Controller
Démarrer Unifi-Controller:

Utilisez 
```
docker-compose up -d
```
Unifi-Controller sera maintenant accessible via l'adresse spécifiée dans le fichier .env (par exemple unifi.domain.tld).  

## Vérification de l'État des Conteneurs  
Tapez la commande suivante pour afficher l'état de tous les conteneurs Docker en cours d'exécution :  
```
docker ps
```
Conteneur en Cours d'Exécution:  
Si vos conteneurs apparaissent dans la liste avec un état "Up", cela signifie qu'ils fonctionnent correctement   

Conteneur Arrêté ou en Erreur:  
Si un conteneur est listé mais n'est pas en état "Up", ou s'il est absent de la liste, cela peut indiquer un problème.  
  
Dans ce cas, vous pouvez utiliser 
```
docker logs [NOM_DU_CONTENEUR]
```
pour obtenir des informations plus détaillées sur le problème.   
