## TP13 - Authentificatio basique
1. Créez deux utilisateurs du proxy, et stocker leurs identifiants dans le fichier /etc/squid/users/list_users. Les utilisateurs seront alice et bob, avec pour mot de passes respectifs alice et bob.


    ```
    sudo mkdir -p /etc/squid/users/
    sudo touch /etc/squid/users/list_users
    htpasswd -m /etc/squid/users/list_users alice
    htpasswd -m /etc/squid/users/list_users bob
    ``` 
2. Configurer squid afin qu'il opère un schéma d'authentification basique avec le programme /usr/lib64/squid/basic_ncsa_auth. La durée de la session doit être de 1 minute. Le message affiché au client sera "servuer proxy de test"
    ``` 
    auth_param basic program /usr/lib64/squid/basic_ncsa_auth /etc/squid/users/list_users
    auth_param basic credentialsttl 1 minute   
    auth_param basic realm servuer proxy de test
    ```     
3. Confiurer une acl staff laissant passer uniquement les utilisateurs connecté.
    ```
    acl staff proxy_auth REQUIRED
    http_access allow staff
    ```
4. Configurez votre client pour passer par squid, et valider qu'on vous demande bien de vous authentifier avant d'utiliser le proxy.
   