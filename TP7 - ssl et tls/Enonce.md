## TP7 - Rechiffrement SSL/TLS


1. Créer un certificat autosigné sur l'url http://website.com/. Vous devrez rediriger tout le trafic http vers du https, ensuite configurez le frontend **generic_frontend** afin qu'il porte le certificat.
   -   Création du certificat et de la clé.
       Renseigner **website.com** au  **Common Name (CN)**
       ```
       $ openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout website_key.pem -out website_cert.pem
       $ cat website_key.pem website_key.pem >> website_cert.pem
       $ sudo mv *.pem /etc/ssl/certs
       $ cd /var/lib/haproxy   # Si HAPproxy est chrooté dans /var/lib/haproxy
       $ sudo mkdir certs
       $ sudo mount --bind certs /etc/ssl/certs
       ```

2. Vos applications **site1** et **site2** tournent à base du serveur web **nginx** dans un conteneur. Mettez en place un certificat autosigné sur **site1** uniquement.

   -   Création du certificat et de la clé pour site1.
       Renseigner **site1.com** au  **Common Name (CN)**.
       ```
       $ openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout site1_key.pem -out site1_cert.pem
       ```
   -   Configuration  du certificat sur site1
       Avant tout, copier le fichier **default.conf** fournit avec l'énoncé dans dans votre répertoire de travail, ensuite faire ceci:
       ```
       $ docker rm -f site1
       $ docker run -d --name site1 -p 81:80 -p 8443:443 site1
       $ docker exec -it site1 mkdir -p /etc/nginx/ssl/
       $ docker cp site1_key.pem site1:/etc/nginx/ssl/
       $ docker cp site1_cert.pem site1:/etc/nginx/ssl/
       $ docker cp default.conf site1:/etc/nginx/conf.d/default.conf
       $ docker restart site1
       ```
    - Vous pouvez testez directement le backend avec l'url https://myproxy.eazytraining.fr:8443/
   
    - Tentez à présent de joindre l'url https://website.com

   