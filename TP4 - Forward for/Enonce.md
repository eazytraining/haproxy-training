## TP4 - Forward-for
1. Sur votre config haproxy, rassurez vous d'avoir la configuration suivante dans votre frontend generic_frontend: 

    ```
    frontend  generic_frontend
        ...
        mode http
        option forwardfor       except 127.0.0.0/8

        # WEBSITE
        acl website_acl hdr_dom(host) -i website.com
        use_backend website if website_acl

        # STUDENTLIST
        acl studentlist_match path -i /pozos/api/v1.0/get_student_ages path -i /pozos/api/v1.0/source_ip
        use_backend studentlist if studentlist_match
        ...
    ```
On peut remarquer l'option **forwardfor** qui envoit l'IP source.

2. Tenter de joindre vos sites 1 et 2 (http://website.com/) et vérifiez les logs applicatifs. Vous devriez voir apparaîre l'ip source dans les logs.


**TIPS**
- Dans Google Chrome, vous pouvez installer l'extension [X-Forwarded-For Header](https://chrome.google.com/webstore/detail/x-forwarded-for-header/hkghghbnihliadkabmlcmcgmffllglin/related), elle servira à forcer l'IP source.
    

3. Sur votre configuration HAProxy, rajouter l'envoie de l'en-tête **Forwarded** dans votre frontend **generic_frontend**. 

4. Vérifiez avec l'url suivante : http://myproxy.eazytraining.fr/pozos/api/v1.0/source_ip. 
**TIPS**
- Regarder le [code application](https://github.com/eazytraining/haproxy-training/blob/main/student-list/simple_api/student_age.py#L42) afin de mieux comprendre ce qui se passe.