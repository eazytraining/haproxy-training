## TP4 - Forward-for
1. Sur votre frontend generic_frontend, rassurez vous d'activer l'**option forwardfor**


2. Tenter de joindre vos sites 1 et 2 (http://website.com/) et vérifiez les logs applicatifs. Vous devriez voir apparaîre l'ip source dans les logs.


    **TIPS**
    - Dans Google Chrome, vous pouvez installer l'extension [X-Forwarded-For Header](https://chrome.google.com/webstore/detail/x-forwarded-for-header/hkghghbnihliadkabmlcmcgmffllglin/related), elle servira à forcer l'IP source.
    

3. Sur votre configuration HAProxy, rajouter l'envoie de l'en-tête **Forwarded** dans votre frontend **generic_frontend**. 

4. Vérifiez avec l'url suivante : http://myproxy.eazytraining.fr/pozos/api/v1.0/source_ip. 

    **TIPS**
    - Regarder le [code application](https://github.com/eazytraining/haproxy-training/blob/main/TP0/student-list/simple_api/student_age.py#L42) afin de mieux comprendre ce qui se passe.