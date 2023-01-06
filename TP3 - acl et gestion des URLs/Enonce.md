## TP3 - ACL et Gestion des URLs

1. Rajouter un nouveau backend nommé **website**, qui va mettre à disposition les applications **site1** et **site2**. Il faudra activer la persistance via la table se session, avec un délai d'expiration de **3s**.

2. Configurer le frontend **webappcolor** comme suit : 
     - il fonctionne en mode **http**
     - il redirige le trafic sur le backend **webappcolor** si l'url est **webappcolor.com**
     - il redirige le trafic sur le backend **website** si l'url est **website.com**

3. Configuer votre dns (fichier hosts) afin de rajouter les entrées website.com et webappcolor.com qui pointent sur l'adresse IP de l'équilibreur de charge. Une fois rajouté, tester le rendu dans votre navigateur.
    - Les applications red et blue devraient être disponibles sur *webappcolor.com*, tandis que les sites 1 et 2 sont disponibles sur *website.com*.

4. Rajouter un nouveau backend nommé **studentlist**, qui va mettre à disposition l'application studentlist.

5. Modifier le frontend **webappcolor** comme suit : 
     - le renommer en **generic_frontend**
     - il va rediriger le trafic vers **studentlist** si la ressource demandée est **/pozos/api/v1.0/get_student_ages**
     - il va rediriger le trafic vers **website** si la ressource demandée est **index.html**
     - le backend par défaut est **website**

6. Pour tester, taper ces urls dans votre navigateur : 
   - http://myproxy.eazytraining.fr → redirige vers site1 et site2
   - http://myproxy.eazytraining.fr/index.html → redirige vers site1 et site2
   - http://website.com/ → redirige vers site1 et site2
   - http://webappcolor.com/ → redirige vers red et blue
   - http://myproxy.eazytraining.fr/pozos/api/v1.0/get_student_ages → redirige vers studentlist

7. Configurer le frontend **generic_frontend** afin que lorsqu'on saisit **http://color.com**, on soit redirigé sur **http://webappcolor.com/** avec le code retour **304**.

    **NB**
    - Attention aux ACLs mises en place à la **question 5**, il pourrait avoir collision, pensez à les commenter **éventuellement**.
    - les méthodes **req.hdr(Host)** et **hdr_dom(host)** sont identiques.
    - N'oubliez de configurer le dns color.com dans votre fichier host avant de faire les tests.
    - Inspectez les pages web de votre navigateur pour voir les code retours et les paramètres de requête.


8. Configurer le frontend **generic_frontend** afin que lorsqu'on saisit **http://myproxy.eazytraining.fr/pozos**, on soit redirigé exactement sur **http://myproxy.eazytraining.fr/pozos/api/v1.0/get_student_ages** avec le codes retour **308**, sans conservation des paramètres de la requête.

9. Rajouter une règle qui envoit automatiquement le trafic vers webappcolor si le **User-Agent** est iphone ou android. La règle doit être la première à etre traitée. De ce fait, l'url http://myproxy.eazytraining.fr/ en tant que client mobile devrait nous montrer les applications red et blue, tandis que la même url avec un client non android ni iphone devrait nous donner les sites web 1 et 2.

    **NB**
    - Vous pouvez changer le **User-Agent** depuis le mode développeur du navigateur google chrome
   