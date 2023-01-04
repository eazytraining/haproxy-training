## TP2 - Persistance de session

1. Dans votre configuration haproxy, activez la table d'affinité de session sur le backend **webappcolor**, puis vérifiez votre configuration HAProxy et recharger la configuration.
    **N.B**
    - *La table de session travaille au niveau **TCP** du modèle OSI, et non HTTP*.
    - L'adresse http://myproxy.eazytraining.com devrait toujours renvoyer sur la même application à chaque appel. 

2. Modifiez le backend webappcolor afin de toujours faire de la persistance, mais cette fois basée sur les cookies de session. Le cookie, nommé **WEBAPCOLOR** sera utilisé uniquement sur le serveur **blue**.
La configuration à mettre en place est ceci : 

3. Une fois la configuration terminée, vérifier que l'url http://myproxy.eazytraining.com reste toujours sur la page rouge et que le cookie **WEBAPCOLOR** est bien présent dans le navigateur.

4. Rajoutez le site1 derrière le backend webappcolor, et configurer la persistance sur ce backend **uniquement**, mais par contre, il faudrait ignorer les resources **.png**, **.css** et **.html**.
La configuration à mettre en place est ceci : 

5. Même si la persistance est activée, elle fonctionne à condition que le backend soit en vie. Stoppez le **site1** et validez que le flux n'est plus envoyé vers ce dernier. 

6. Forcez le trafic afin qu'il soit toujours routé vers **site1**.


**N.B**
    Pour forcer la redirection vers site1, l'url est la suivante : http://myproxy.eazytraining.com/?serv=1&offline=true
    