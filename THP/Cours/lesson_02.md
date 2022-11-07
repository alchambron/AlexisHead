# Fly.io : Hebergeur gratuit

Voici un petit tuto d'installation et de mise en place de Fly.io, un hébergeur gratuit et simple d'utilisation !

## 1\. Introduction

Avec le passage d'Heroku en payant, je me dois de te faire un tutoriel sur un hébergeur gratuit, n'oublie pas qu'énormément de cours sont écrits sous Heroku, c'est voulu, ça reste le best du best. Mais pas d'inquiétude, si tu ne souhaites pas payer, ce tuto est fait pour toi ! Fly.io permet de déployer ton site en Rails 7.

## 2\. La ressource

### 2.1\. Installation

Avant de commencer à utiliser Fly.io, il faut que tu l'installes.

#### 2.1.1\. Mac

Si tu es sur mac et que tu utilise Homebrew, lance :
```shell
  $ brew install flyctl
```

Sinon fait :
```shell
  $ curl -L https://fly.io/install.sh | sh
```

#### 2.1.2\. Linux & WSL

Dans le cas ou tu utilise linux ou n'importe quel wsl, lance :
```shell
  $ curl -L https://fly.io/install.sh | sh
```
___
 ⚠️ **ALERTE ERREUR COMMUNE**

N'oublie pas de penser à lire ce que te dis ton terminal, il se pourrait que Fly.io ne fonctionne pas correctement si tu oublies de faire ce que ton terminal t'indique. Pour ma part j'ai reçu ceci en fin d'installation : 
```shell
  flyctl was installed successfully to /root/.fly/bin/flyctl
  Manually add the directory to your $HOME/.bash_profile (or similar)
    export FLYCTL_INSTALL="/root/.fly"
    export PATH="$FLYCTL_INSTALL/bin:$PATH"
  Run '/root/.fly/bin/flyctl --help' to get started
```

J'ai donc pris la peine de faire les 2 exports proposées. Maintenant si je fais `flyctl --help` sans passer par son chemin, cela fonctionne
___

### 2.2\. Création de ton compte

Rien de plus simple, pour cela il te suffit de te faire cette commande :
```shell
  $ flyctl auth signup
```

Ensuite cela t'ouvre une page web, inscrit toi avec ton compte github ! Cela devrais également te connecté automatiquement

### 2.3\. Se connecter

Si tu n'as pas été connecté à l'étape précédente, tu as juste à envoyer ceci sur ton terminal :
```shell
  $ flyctl auth login
```

### 2.4\. Initialisation d'une application

Tu dois tout d'abord activé wireguard et websockets, sans ça, cela ne fonctionneras pas
```shell
  $ fly wireguard websockets enable
```

Rien de plus simple, il te suffit simplement de lancer :
```shell
  $ fly launch
```

Une multitude d'option vont s'afficher une par une, je vais les décortiquer avec vous :

- La première étape sera de donner un nom à ton app :
  ```shell
    Choose an app name (leave blank to generate one):
  ```
  Par exemple `tutothp`
- Ensuite tu dois choisir ta région de déploiement :
  ```shell
    Choose a region for deployment:  [Use arrows to move, type to filter]
  ```
  C'est de base au plus proche de la ou tu es, donc `Paris, France 'cdg'`
- Après l'application te demande si tu veux créer une base de données postreSQL :
  ```shell
    Would you like to set up a Postgresql database now? (y/N)
  ```
  La réponse est oui `y`
- Enfin, on te propose quel type de déploiement tu souhaite utiliser pour ton application :
  ```shell
    Select configuration:  [Use arrows to move, type to filter]
      >   Development - Single node, 1x shared CPU, 256MB RAM, 1GB disk
      Production - Highly available, 2x shared CPUs, 4GB RAM, 40GB disk
      Production - Highly available, 4x shared CPUs, 8GB RAM, 80GB disk
      Specify custom configuration
  ```
  Ici tu prendras la première option, car tu ne souhaites pas utiliser ta carte bleue et tu es bien là pour tester du code qui est en cours de développement 

___
 ⚠️ **ALERTE ERREUR COMMUNE**

Si jamais ta console t'affiche une erreur lors de la création de ta base de données postgresql, de ce genre :
```shell
  Setting secrets on app test-deploy-thp-db...Provisioning 1 of 1 machines with image flyio/postgres:14.4
  Failed creating the Postgres cluster test-deploy-thp-db: failed to launch VM: Post "http://[fdaa:0:cd8e::3]:4280/v1/apps/test-deploy-thp-db/machines": connect tcp [fdaa:0:cd8e::3]:4280: operation timed out
  Your Rails app is prepared for deployment.
```

Tu peux toujours essayer de comprendre le souci en faisant un `fly doctor` ou en te rendant directement sur le site communautaire de [fly.io](https://community.fly.io)
___

___
 ⚠️ **ALERTE ERREUR COMMUNE BIS**

L'utilisation de VPN peut totalement bloquer le système proposé par fly.io
___

Normalement, après tout ça, c'est bon pour toi, ta base de données postgresql et ton application sont maintenant en ligne !

### 2.5\. Utilisation de Fly.io

Maintenant que ton site est en ligne il serait bon de pouvoir utiliser la console de fly pour lancer ta seed par exemple.

Voici la commande pour avoir accès à la console de fly
```shell
  $ fly ssh console
```

Une fois dedans tu peux lancer ta seed ainsi :
```shell
  $ /app/bin/rails db:seed
```

Si tu veux accéder directement à la console rails tu peux faire :
```shell
  $ fly ssh console -C "/app/bin/rails console"
```

Et si tu veux ouvrir ton application directement par ta console tu as juste à faire :
```shell
  $ fly open
```

## 3\. Pour aller plus loin

- Je sais que l'incroyable Deanin a fait une vidéo qui explique la création [d'un site de e-commerce + du déployement de fly.io](https://www.youtube.com/watch?v=ZHVvjBNi41E)
- Tu peux toujours aller faire un tour sur la [documentation de fly.io](https://fly.io/docs/)