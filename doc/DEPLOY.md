# Procédure de Déploiement Grégory MAJSTOROVIC

## Se connecter à l'application

admin@ht-buggy-wapp.fr
user@ht-buggy-wapp.fr

mot de passe : azertyuiop

## Installation aapanel

Commande :

```bash
URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh aapanel
```

Une fois installé j'ai clique sur le lien "aaPanel Internal Address: <https://172.17.4.14:17111/7d1347f0>"

Et il me donne les identifiants :

- user : **8yua1sar**
- password : **de31f18b**

Il m'ouvre le dashboard de aapanel, je me connecte avec les identifiants et ensuite j'ai cliqué sur le "One click" pour installé le pack LNMP.

## Création du site sur aapanel

Sur aapanel je me rend dans Website puis je clique sur "add site".
Dans le formulaire, je met mon nom de domaine "majstorovic-dfsgr1.local" et je créer la base de données mysql

Pour que toutes les pages fonctionnent, j'ai du aller dans URL rewrite et sélectionner Laravel.

## Gitcliff

Gitcliff étant déjà initialisé dans le projet, j'ai juste fait :

```bash
git cliff --bump -o CHANGELOG.md
```

pour mettre à jour le fichier changelog après avoir commit, j'ai aussi créer un tag 1.0.0 avec la commande

```bash
git tag 1.0.0
```

```bash
git remote add vps root@172.17.4.14:/var/depot_git
```

Pousser :

```bash
git push vps <version>
```

puis yes pour accepter.

## Préparation du VPS

### Depot git sur le SSH

Je vais initialiser le repo git sur le serveur.
Pour ça je fais :

```bash
cd /var
mkdir depot_git
cd depot_git
git init --bare
```

Création du deploy.sh

```bash
touch deploy.sh
nano deploy.sh
```

Et dedans je met :

```sh
git --work-tree=/www/wwwroot/gregory --git-dir=/var/depot_git checkout -f $1
```

"gregory" c'est le nom du site que j'ai mis sur aapanel

## Méthode de déploiement

Pour déployer, en local je fais :

```bash
git remote add vps root@172.17.4.14:/var/depot_git
```

puis

```bash
git push -u vps <version>
```

et sur serveur je fais :

```bash
bash deploy.sh <version>
```

## Swagger

```bash
composer require zircote/swagger-php
```
