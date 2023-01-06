## TP5 - Healtcheck et gestion des erreurs
Les objectifs de ce TP sont les suivants : 
- Configurer les tests de vie
- Gérer les erreurs

## Documentation 
- Voici un lien vers la fonctionnalité X : http://someurl.com

#### Prérequis : 
- Avoir finalisé le **TP X**
#### Instructions

1. Sur votre backend webappcolor, configurer un check TCP sur le serveur **red**, à intervalle de 5s, avec une sortie du serveur à 2 échec et une remise du serveur dans le flux à 4 health checks en succès.
La configuration à rajouter:
    ```
    frontend generic_frontend
        ...
        # WEBAPP COLOR
        acl webappcolor_acl hdr_dom(host) -i webappcolor.com
        use_backend webappcolor if webappcolor_acl
    
    backend webappcolor
        ...
        balance roundrobin
        server red    localhost:8080 check inter 5s fall 2 rise 4
        server blue   localhost:8081 check
        ...
    ```
2. Stoppez l'application red et vérifiez que le serveur est enlevé du flux au bout de 10 sec maximum, et remmis dans le flux au bout de 20 sec minimums. Le test se fera sur l'url http://webappcolor.com. Pour stopper ou démarrer l'appli red :
    ```
    docker stop red    # stopper l'application
    docker start red   # démarrer l'application
    ```    

    ---
    **TIPS**
    - Le fichier **11-haproxy.cfg** pourrait vous inspirer
    - Seule l'application **bleu** répondra, le client n'aura pas d'erreur, car on a enlevé le serveur défaillant du trafic.

    ---
3. Sur le backend website, mettre en place un check http sur la page index.html, avec comme message attendu **Dimension** ou **Favorite**. Il faudra utiliser la méthode GET au lieu du HEAD, afin de récupérer le contenu de la réponse. La configuration à mettre en place est la suivante: 

    ```
    frontend generic_frontend
        ...
        # WEBSITE
        acl website_acl hdr_dom(host) -i website.com
        use_backend website if website_acl

    backend website
        mode http
        balance     roundrobin
        server  site2 127.0.0.1:82 check
        server  site1 127.0.0.1:81 check
        stick-table type ip size 1m expire 3s
        stick match src
        stick store-request src
        http-check expect rstring (Dimension|Favorite)
        option httpchk GET /index.html
    ```
    Vous pouvez tester avec http://website.com.


4. Configurez un nouveau backend ihm_studentlist, vers qui on enverra le traffic si le client saisit http://mystudentlist.com. On en profitera pour mettre en place un health check sur l'IHM, qui dépendra de l'état de vie de son serveur backend nommé **studentlist_server1**, localisé dans le backend **studentlist** de HAProxy. Voici la configuration nécessaire

    ```
    frontend generic_frontend
        ...
        # IHM STUDENTLIST 
        acl ihm-api_acl hdr_dom(host) -i studentlist.com
        use_backend ihm_studentlist if ihm-api_acl    
        ...
    
    backend ihm_studentlist
        ...
        server  ihm-api 127.0.0.1:83 track studentlist/studentlist_server1
        ...

    backend studentlist
        ...
        server  studentlist_server1 127.0.0.1:5000 check        
        ...
    ```
5. Stoppez l'application studentlist, et vérifiez que son ihm répondra une erreur 503. Pour stopper studenlist, taper ceci : 
    ```
    docker stop api
    ```            
   
6. Modifiez le backend ihm_studentlist en ajoutant les applications red et blue. red et blue seront tous deux backups. La configuration serait ceci : 
    ```
    backend ihm_studentlist
        ...
        server  red     localhost:8080 check backup
        server  blue    localhost:8081 check backup
        server  ihm-api localhost:83   check
        server  studentlist_server1 127.0.0.1:5000 track studentlist/studentlist_server1
        option  allbackups
        ...
    ```
7. Testez l'url http://mystudentlist.com, elle devrait vous donner l'ihm de studentlist. Stoppez l'ihm refaites le test, on devrait voir une bascule entre les application red et blue.

#### Récapitulatif
Vous avez mis en place les principes de test de vie avec HAProxy, ainsi que la mise en place de serveur secondaire.
   