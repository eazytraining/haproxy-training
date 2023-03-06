## TP11 - Installation de squid
1. Sur votre VM **squid** déployée au **TP0**, installer **squid**. 
    ```
    sudo yum install squid -y
    ```
2. Une fois installé, éditer la configuration afin d'écouter sur le port ```3128```, et activer la gestion de la cache.

3. Vérifier que la configuration ne comporte aucune erreur, ensuite démarrer le service et vérifier qu'il est bien fonctionnel
    ```bash
    systemctl start squid
    squidclient  http://192.168.99.10  | grep -iE "favo|dime"
    ```