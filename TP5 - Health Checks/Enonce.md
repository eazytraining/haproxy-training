## TP5 - Healtcheck et gestion des erreurs

1. Sur votre backend **webappcolor**, configurer un check TCP sur le serveur **red**, à intervalle de 5s, avec une sortie du serveur à 2 échec et une remise du serveur dans le flux à 4 health checks en succès.

2. Stoppez l'application red et vérifiez que le serveur est enlevé du flux au bout de 10 sec maximum, et remmis dans le flux au bout de 20 sec minimum. Le test se fera sur l'url http://webappcolor.com. Voici les commandes permettand de stopper ou démarrer l'appli red :
    ```
    docker stop red    # stopper l'application
    docker start red   # démarrer l'application
    ```    

3. Sur le backend **website**, mettre en place un check http sur la page index.html, avec comme message attendu **Dimension** ou **Favorite**. Il faudra utiliser la méthode GET au lieu du HEAD, afin de récupérer le contenu de la réponse. Vous pouvez tester avec http://website.com.


4. Configurez un nouveau backend **ihm_studentlist**, vers qui on enverra le traffic si le client saisit http://mystudentlist.com. On en profitera pour mettre en place un health check sur l'IHM, qui dépendra de l'état de vie de son serveur backend nommé **studentlist_server1**, localisé dans le backend **studentlist** de HAProxy.

5. Stoppez l'application studentlist, et vérifiez que son ihm répondra une erreur 503. Pour stopper studenlist, taper ceci : 
    ```
    docker stop api
    ```            
   
6. Modifiez le backend **ihm_studentlist** en ajoutant les applications red et blue. red et blue seront tous deux backups. 

7. Testez l'url http://mystudentlist.com, elle devrait vous donner l'ihm de studentlist. Stoppez l'ihm et refaites le test, on devrait voir une bascule entre les application red et blue.