# Configuration des Services Docker avec le Dépôt dkr.ase_vps

## Objectif:
Cloner le dépôt dkr.ase_vps pour configurer rapidement les services Docker tels que Traefik, Portainer et Unifi-Controller.


## Prérequis :
Docker-compose installés.  
Nano installé.  
Git installé.

## Étape 0: Préparation de l'Environnement de Travail
Allez a la racine 

Utilisez
```
cd /
```

Créer un dossier pour tout les docker-compose  

Utilisez
```
mkdir docker
```

Allez dans le dossier du docker-compose

Utilisez
```
cd /docker
```

## Étape 1: Clonage du Dépôt
Exécutez la commande suivante pour cloner le dépôt :

Utilisez 
```
git clone https://github.com/sidlaunay/dkr.ase_vps/
```

Naviguez dans le dossier cloné  

Utilisez 
```
cd dkr.ase_vps
```

Copie des Dossiers dans /docker/  

Utilisez 
```
cp -r traefik/ portainer/ unifi-controller/ /docker/
```

Allez dans le répertoire /docker/

Utilisez 
```
cd /docker
```

Contrôlez la présence des dossiers

Utilisez 
```
ls
```


## Étape 2: Configuration de Traefik
### Étape 2.0: Allez dans le répertoire traefik:

Une fois le "ls" effectué "traefik" doit apparaître  

Utilisez
```
cd traefik/
```

Voir la liste de fichiers présents  
Utilisez 
```
ls
```

### Étape 2.1: Modifier traefik.toml:

Utilisez
```
nano traefik/traefik.toml
```

Remplacez "email@domain.tld" par votre adresse e-mail.  

### Étape 2.2: Configuration Avancée avec traefik_dynamic.toml:

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
Copiez le résultat (ex. user:$2y$05$...) dans traefik_dynamic.toml  

Utilisez
```
nano traefik_dynamic.toml
```
  
Configurer l'authentification et les routes:  
Remplacez user:htpasswd_password par le résultat de htpasswd.  
Changez trae.domain.tld par votre domaine

### Étape 2.2: Création de acme.json

Créer acme.json:  
Utilisez 
```
touch acme.json  
```

Sécurisez le fichier avec 

```
chmod 660 acme.json
```

Démarrer traefik:

Utilisez 
```
docker-compose up -d
```
Unifi-Controller sera maintenant accessible via l'adresse spécifiée dans le fichier .env (par exemple trae.domain.tld).  


## Étape 3: Configuration de Portainer

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
