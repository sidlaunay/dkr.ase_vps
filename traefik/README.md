# Configuration de Traefik via Docker-Compose

## Objectif:
Installer et configurer Traefik comme reverse proxy pour les conteneurs Docker.

## Prérequis :
Docker-compose installés.  
Nano installé.

## Étape 0: Préparation de l'Environnement de Travail
Créer un dossier pour le docker-compose  

Utilisez
```
mkdir traefik
```

Allez dans le dossier du docker-compose

Utilisez
```
cd traefik
```

## Étape 1: Création et Configuration de http.yml
Créer le fichier http.yml:  
Utilisez 
```
nano http.yml  
```
Copiez-y le contenu fourni pour la configuration des middlewares HTTP.

## Étape 2: Configuration de tls.yml
Créer le fichier tls.yml:  
Utilisez 
```
nano tls.yml  
```
Insérez la configuration TLS fournie.

## Étape 3: Configuration de traefik.toml
Créer et configurer traefik.toml:  
Utilisez 
```
nano traefik.toml  
```
Ajoutez le contenu, en remplaçant "email@domain.tld" par votre adresse e-mail.

## Étape 4: Configuration Avancée avec traefik_dynamic.toml
Installer Apache2-utils:  
Exécutez 
```
apt install apache2-utils  
```
  
Créer un utilisateur:  
Utilisez 
```
htpasswd -nB [USERNAME]
```
pour générer un mot de passe.  
Copiez le résultat (ex. user:$2y$05$...) dans traefik_dynamic.toml.  
  
Configurer l'authentification et les routes:  
Remplacez user:htpasswd_password par le résultat de htpasswd.  
Changez trae.domain.tld par votre domaine.  

## Étape 5: Docker-compose
Créer et configurer docker-compose.yml:  
Utilisez 
```
nano docker-compose.yml  
```
Insérez le contenu de configuration.  

## Étape 6: Création de acme.json
Créer acme.json:  
Utilisez 
```
touch acme.json  
```
Sécurisez le fichier avec 
```
chmod 660 acme.json
```

## Étape 7: Lancement de Traefik
Démarrer Traefik:  
Exécutez 
```
docker-compose up -d  
```
Vérifiez le fonctionnement correct de Traefik.  
Connectez-vous via le domaine défini.
  
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

