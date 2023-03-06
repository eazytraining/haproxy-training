## TP10 - HAProxy et Keepalived

1. Mettez en place un deuxième serveur HAProxy, dans le même réseau que le premier, leur configurations doivent être identique.
2. Installez et configurez keepalived sur les deux serveurs, avec une IP flottante au choix dans votre réseau privé.<br>Les configurations sont données:
   - **keepalived-1.conf** pour le serveur **PRIMAIRE**
   - **keepalived-2.conf** pour le serveur **SECONDAIRE**
3. N'oubliez de modifier la configuration kernel.
4. Activer la table de session et configurez la synchronisation de celle ci entre les serveurs HAProxy.
5. Vérifiez que les deux serveurs ont bien la même table avec les commandes suivantes tapée sur chaque serveur: 
    ```
    sudo yum install socat -y
    echo "show table website" | sudo socat stdio /var/run/haproxy.sock
    ```
   