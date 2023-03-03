## TP9 - Gestion des logs et des pages d'erreur

1. Activer le logging haproxy sur **127.0.0.1**, avec l'identifiant ```local2```, et la facilité ```info```.

2. Configurer le démon rsyslog afin qu'il capture ces logs et les enregistre dans les fichiers **/var/log/haproxy-traffic.log** et **/var/log/haproxy-admin.log** pour respectivement ```local2.*``` et ```local2.notice```. 
3. N'oubliez pas de redémarrer le **rsyslog** et **HAProxy**
    ```
    sudo systemctl restart rsyslog
    sudo systemctl reload haproxy
    ```
4. Vérifier que les journaux sont bien présents dans les fichiers adéquats.

5. Créer des pages d'erreurs personnalisées pour les codes retour **503** et **403**  dans **/etc/haproxy/errorfiles**. Une fois fait, configurer Haproxy afin qu'il utilise ces pages d'erreur.


   