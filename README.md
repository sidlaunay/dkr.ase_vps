# Configuration des Services Docker avec le Dépôt dkr.ase_vps

## Objectif:
Cloner le dépôt dkr.ase_vps pour configurer rapidement les services Docker tels que Traefik, Portainer et Unifi-Controller.


## Prérequis :
Docker-compose installés.  
```
apt install docker-compose
```
Nano installé.  
```
apt install nano
```
Git installé.  
```
apt install git
```
Curl installé.  
```
apt install curl
```

## Étape 0: Préparation de l'Environnement de Travail
Allez à la racine 

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

Allez dans le dossier "docker" et contrôlez la présence des dossiers

Utilisez 
```
cd /docker
```

Utilisez 
```
ls
```

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
nano traefik.toml
```

Remplacez "email@domain.tld" par votre adresse e-mail.  

Pour quitter "nano" faites "CTRL"+"X" ensuite "Y" et "ENTER"  

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
Copiez le résultat (ex. user:$2y$05$...) dans traefik_dynamic.toml pour remplacer "user:htpasswd_password"  

Utilisez
```
nano traefik_dynamic.toml
```
  
Configurer l'authentification et les routes:  
Remplacez "user:htpasswd_password" par le résultat de htpasswd.  
Changez "trae.domain.tld" par votre domaine "FQDN"

Pour quitter "nano" faites "CTRL"+"X" ensuite "Y" et "ENTER"  

### Étape 2.2: Création de acme.json:

Créer acme.json:  
Utilisez 
```
touch acme.json  
```

Sécurisez le fichier avec 

```
chmod 600 acme.json
```
### Étape 2.3: Configuration du DNS:

Récupérez l'ip publique de la machine afin de faire un enregistrement chez votre fournisseur DNS  

Utilisez 

```
curl ifconfig.net
```

Ensuite allez sur le site de votre hébergeur DNS afin de faire un enregistrement de "type A"

example: trae.domain.tld = [IP PUBLIQUE]

### Étape 2.4: Démarrer traefik:

Utilisez 
```
docker-compose up -d
```
Unifi-Controller sera maintenant accessible via l'adresse spécifiée dans le fichier "traefik_dynamic.toml" (par exemple trae.domain.tld).  


## Étape 3: Configuration de Portainer  
### Étape 3.0: Allez dans le répertoire Portainer:  
Allez dans le dossier "docker" et contrôlez la présence des dossiers  

Utilisez 
```
cd /docker
```

Utilisez 
```
ls
```

Une fois le "ls" effectué "portainer" doit apparaître  

Utilisez  
```
cd portainer/
```

Voir la liste de fichiers présents  
Utilisez 
```
ls
```

### Étape 3.1: Configuration du Fichier .env pour Portainer  

Allez dans le fichier ".env"

```
nano .env
```

Remplacez "port.domaine.tld" par votre domaine "FQDN" sur la ligne "TREAFIK_FQDN="  

Pour quitter "nano" faites "CTRL"+"X" ensuite "Y" et "ENTER"  

### Étape 3.2: Configuration du DNS:

Récupérez l'ip publique de la machine afin de faire un enregistrement chez votre fournisseur DNS  

Utilisez 

```
curl ifconfig.net
```

Ensuite allez sur le site de votre hébergeur DNS afin de faire un enregistrement de "type A"

example: port.domain.tld = [IP PUBLIQUE]  

### Étape 3.3: Démarrer Portainer:
Utilisez 
```
docker-compose up -d
```
Portainer sera maintenant accessible via l'adresse spécifiée dans le fichier .env (par exemple port.domain.tld).

## Étape 4: Configuration de Unifi-controller  
### Étape 4.0: Allez dans le répertoire Unifi-controller:
Allez dans le dossier "docker" et contrôlez la présence des dossiers  

Utilisez 
```
cd /docker
```

Utilisez 
```
ls
```

Une fois le "ls" effectué "unifi-controller" doit apparaître  

Utilisez  
```
cd unifi-controller/
```

Voir la liste de fichiers présents  
Utilisez 
```
ls
```

### Étape 4.1: Configuration du Fichier .env pour Unifi-controller  

Allez dans le fichier ".env"

```
nano .env
```

Remplacez "unifi.domaine.tld" par votre domaine "FQDN" sur la ligne "TREAFIK_FQDN="  
Ajoutez votre mot de passe, en remplaçant "password" par votre mot de passe sur la ligne "DB_PASSWD="  
(Pas de caractère spéciaux)


Pour quitter "nano" faites "CTRL"+"X" ensuite "Y" et "ENTE

### Étape 4.2: Configuration du DNS:

Récupérez l'ip publique de la machine afin de faire un enregistrement chez votre fournisseur DNS  

Utilisez 

```
curl ifconfig.net
```

Ensuite allez sur le site de votre hébergeur DNS afin de faire un enregistrement de "type A"

example: port.domain.tld = [IP PUBLIQUE]

### Étape 4.3: Démarrer Unifi-Controller:
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
