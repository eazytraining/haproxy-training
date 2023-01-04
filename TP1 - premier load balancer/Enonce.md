## TP1 - déploiement d’un équilibreur de charge

1. Sur votre VM déployée au TP0, installer haproxy. N'oubliez pas de le démarrer et rendre son service enable :

2. Dans le fichier de configuration, mettez en place un reverse proxy tel que : 
   - Le port d'écoute est le **80**
   - Le frontend se nomme **webappcolor** et redirige le trafic le backend **webappcolor**.

3. Une fois configuré, testez la validité de votre configuration et visualisez le résultat dans un navigateur à l'adresse http://myproxy.eazytraining.com


4. Rajoutez l'application **blue** dans le backend **webappcolor** afin de mettre en place un équilibreur de charge entre les applications **red** et **blue** du backend **webappcolor**.

5. Mettez en place un listen nommé **admin**  afin d'activer d'activer la page de statistiques comme suit : 
   - L'accès sera authentifié 
     - login: **admin** 
     - password: **password**
   - L'url d'accès sera **/admin**
   - Le port d'accès sera le **10000**
   - Les utilisateurs connectés auront tous les droits
   