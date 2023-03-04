## Mini projet squid

### Présentation de l'infrastructure.
Soit le schéma d'architecture réseau suivant:<br>
![Archi mini projet](img/architecture_mini_projet.jpg).
<br>
Trois sous-réseaux sont définis pour les stations clientes.<br>Les serveurs sont dans leur propre sous-réseau ayant pour adresse **172.16.0.0** et le proxy possède l’adresse **172.16.1.12**. Le routage entre ces sous-réseaux se fait par un commutateur de niveau 3.<br>
On désire que le sous-réseau administratif puisse avoir accès au serveur proxy aux heures de bureau (plage horaire allant de **7h30** à **19h30**). Les clients du pôle chimie ont accès au serveur proxy du **lundi au samedi** alors que les utilisateurs du service informatique doivent avoir accès en permanence au serveur proxy pour naviguer sur Internet.

### Partie I: accès au proxy
1. Donner les acl permettant de déclarer les sous-réseaux des trois services présents sur le réseau local.

2. Donner les acl permettant de définir les heures de bureau qui seront appliquées au service administratif et les jours de fonctionnement pour les utilisateurs du pôle chimie.

3. Donner les règles d'accès avec la directive ```http_access```.


Les manipulation précédentes nous ont permises de déclarer des utilisateurs et de les autoriser ou non à accéder au proxy, donc indirectement à Internet, en fonction de plages horaires.

Il faut à présent faire en sorte que les utilisateurs du pôle chimie et du réseau administratif ne puissent consulter des sites possédant les mots sexe, violent dans l’URL. Ils n’auront pas non plus le droit de télécharger des objets audio ou vidéo. De plus, les utilisateurs du pôle administratif ne pourront pas accéder à des sites FTP. 

### Partie II: restriction d'url
1. Créez les ACL basées sur les expressions régulières qui permettent de définir les sites avec les mots sexes et violent et celles interdisant le téléchargement d’objets audio ou vidéo.

2. Créez un ACL définissant le protocole FTP.

3. Modifiez les règles d’accès pour que les conditions définies dans l’exemple soient appliquées.


:warning: Vous ne pouvez pas disposer les règles d’accès de n’importe quelle façon. Ne perdez pas de vue qu’elles sont lues de manière séquentielle et qu’une règle mal positionnée pourrait avoir l’effet inverse de celui voulu.


4. Si vous êtes convaincu de votre travail, donnez le fichier de configuration complet de votre serveur squid.
