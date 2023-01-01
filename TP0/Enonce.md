## TP0 : Déploiement du labs de travail
#### Objectifs du TP
Les objectifs de ce TP sont les suivants : 
- Déployer l'environnement de travail
- Installer les applications fil rouges

#### Prérequis : 
- Avoir un PC performant
- Avoir installé git, virtualbox et vagrant sur son PC
   -  vbox : https://download.virtualbox.org/virtualbox/6.1.40/VirtualBox-6.1.40-154048-Win.exe
   -  vagrant : https://releases.hashicorp.com/vagrant/2.3.4/vagrant_2.3.4_windows_amd64.msi
   -  git : https://github.com/git-for-windows/git/releases/download/v2.38.1.windows.1/Git-2.38.1-64-bit.exe


#### Instructions
1. Sur votre poste de travail, exécutez les commandes suivantes : 

   ```
   git clone https://github.com/diranetafen/cursus-devops.git 
   cd vagrant/haproxy-squid
   vagrant up --provision
   vagrant ssh haproxy
   vagrant ssh squid
   ```
  
2. Créer une entrée DNS **myproxy.eazytraining.com** dans les fichiers hosts de votre machine physique et de vos VMs. Cette entrée pointera vers l'adresse IP de la VM haproxy.
  
#### Récapitulatif

##### Sur la VM haproxy
Nous avons déployé 5 applications sur la VM Haproxy: 
- red : disponible sur le port **8080**
- blue : disponible sur le port **8081**
- site1 : disponible sur le port **81**
- site2 : disponible sur le port **82**
- studentlist: disponible sur les ports **83** (IHM) et **5000** (Backend)

```
$ docker ps -a 
CONTAINER ID   IMAGE                    COMMAND                  CREATED             STATUS             PORTS                                       NAMES
633ec16aaf98   php:apache               "docker-php-entrypoi…"   12 minutes ago      Up 12 minutes      0.0.0.0:83->80/tcp, :::83->80/tcp           ihm-api
6e85189ef0fe   student-list             "python ./student_ag…"   14 minutes ago      Up 14 minutes      0.0.0.0:5000->5000/tcp, :::5000->5000/tcp   api
d7c47fb5ae0e   site1                    "/usr/sbin/nginx -g …"   24 minutes ago      Up 24 minutes      0.0.0.0:81->80/tcp, :::81->80/tcp           site1
39101101c82b   site2                    "/usr/sbin/nginx -g …"   27 minutes ago      Up 27 minutes      0.0.0.0:82->80/tcp, :::82->80/tcp           site2
ea10a6c40203   kodekloud/webapp-color   "python app.py"          About an hour ago   Up About an hour   0.0.0.0:8081->8080/tcp, :::8081->8080/tcp   blue
bb5e3d70de85   kodekloud/webapp-color   "python app.py"          About an hour ago   Up About an hour   0.0.0.0:8080->8080/tcp, :::8080->8080/tcp   red
```


Ces applications seront utilisées durant la formation.

##### Sur la VM squid
Nous avons simplement installé squid. Cette VM  sera utilisée dans la deuxième partie du programme.
