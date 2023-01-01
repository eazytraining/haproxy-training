## TP1 - déploiement d’un équilibreur de charge
Les objectifs de ce TP sont les suivants : 
- Installer haproxy sur centos
- Se familiariser avec la configuration de l'outil
- Mettre en place son premier proxy inversé (reverse proxy)
- Mettre en place son premier équilibreur de charge (Load Balancer)

## Documentation 
- https://www.haproxy.org/download/2.7/doc/configuration.txt


#### Instructions

1. Sur votre VM déployée au TP0, installer haproxy. N'oubliez pas de le démarrer et rendre son service enable :

2. Dans le fichier de configuration, mettre en place un reverse proxy tel que : 
   - Le port d'écoute est le **80**
   - Le frontend se nomme **webappcolor** et redirige le trafic au  afin de mettre en place un équilibreur de charge entre les application **red**backend **webappcolor** et blue
   - L'application **red** (**port 8080**) est dans le backend **webappcolor**

3. Une fois configuré, tester la validité de votre configuration et visualisez le résultat dans un navigateur à l'adresse http://myproxy.eazytraining.com


4. Rajoutez l'application **blue** dans le backend **webappcolor** afin de mettre en place un équilibreur de charge entre les applications **red** et **blue**.
   