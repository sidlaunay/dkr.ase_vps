# Configuration de Portainer avec Traefik via Docker-Compose

## Objectif:
Installer et configurer Portainer, une interface de gestion de conteneurs Docker, avec Traefik comme reverse proxy.

## Prérequis :
Docker-compose installés.  
Nano installé.

## Étape 0: Préparation de l'Environnement de Travail
Créer un dossier pour le docker-compose  

Utilisez
```
mkdir portainer
```

Allez dans le dossier du docker-compose

Utilisez
```
cd portainer
```

## Étape 1: Configuration du Fichier .env pour Portainer
Créer le fichier .env  

Utilisez 
```
nano .env
```
Ajoutez le contenu, en remplaçant port.domaine.tld par votre domaine FQDN sur la ligne "TREAFIK_FQDN="  

## Étape 2: Création et Configuration de docker-compose.yml pour Portainer
Créer et configurer docker-compose.yml pour Portainer:

Utilisez 
```
nano docker-compose.yml
```
Copier le contenu.

## Étape 3: Lancement de Portainer
Démarrer Portainer:

Utilisez 
```
docker-compose up -d
```
Portainer sera maintenant accessible via l'adresse spécifiée dans le fichier .env (par exemple port.domain.tld).  

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
