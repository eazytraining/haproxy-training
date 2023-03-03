## TP10 - HAProxy et Keepalived

1. Mettez en place un deuxième serveur HAProxy, dans le même réseau que le premier, leur configurations doivent être identiques: 
2. Installez et configurez keepalived sur les deux serveurs, avec une IP flottante au choix dans votre réseau privé. Les configurations sont données:
   - **keepalived-1.conf** pour le serveur PRIMAIRE
   - **keepalived-2.conf** pour le serveur SECONDAIRE
3. N'oubliez de modifier la configuration kernel. La configuration est la suivante :
    ```
    echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf
    echo "net.ipv4.ip_nonlocal_bind=1" >> /etc/sysctl.conf
    echo "net.ipv4.all.arp_announce=2" >> /etc/sysctl.conf
    echo "net.ipv4.all.arp_ignore=1" >> /etc/sysctl.conf    
    sysctl -p /etc/sysctl.conf
    ```

    
    ---
    **TIPS**
    Vous pouvez aussi prendre le fichier **etc/sysctl.d/haproxy.conf** fournit avec l'énoncé et le déposer dans **/etc/sysctl.d/haproxy.conf**, ainsi que le fichier **etc/security/limits.conf** à mettre au même endroit sur le serveur, et enfin recharger la configuration kernel.
    Cette configuration se rapproche d'une configuration d'entreprise.

    ---    

4. Activer la table de session et configurez la synchronisation de celle ci entre les serveurs HAProxy.

5. Vérifiez que les deux serveurs ont bien la même table, avec la commande suivante tapée sur chaque serveur :     
    ```
    echo "show table website" | sudo socat stdio /var/run/haproxy.sock
    ```   

#### Récapitulatif
A la fin de ce TP, vous avez mis en place la haute disponibilité sur un cluster HAProxy
   