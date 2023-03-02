## TP8 - Authentification et blacklistage

1. Mettez en place de l'authentification avec un mot de passe chiffré dans la configuration HAProxy.<br>Les utilisateurs à créer sont **dirane** (password = **mypassword123**) et **ulrich** (password = **anotherpassword**).<br>Voici les commandes permettant de chiffrer le mot de passe:
    ```
    $ docker run -itd --name test ubuntu:18.04 
    $ docker exec -it test apt update -y
    $ apt install whois 
    $ docker exec -it test apt install whois 
    $ docker exec -it test mkpasswd -m sha-256 mypassword123 
    $ docker exec -it test mkpasswd -m sha-256 anotherpassword  
    ```

2. Connectez vous à https://website.com pour tester celà.

3. Configurer HAProxy afin qu'il refuse du traffic en provenance de 127.0.0.1