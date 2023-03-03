## TP12 - Filtrage avec squid
1. Mettez en place une acl (website) squid qui interdit le trafic vers http://website.com/ 
    ```
    acl website dstdomain .website.com
    http_access deny website
    ```   
2. Mettez en place des acls (website et blacklist) squid qui interdisent le trafic vers http://website.com/ en provenance du réseau d'adresse IP 172.28.128.0/24
    ```
    acl blacklist src 172.28.128.0/24
    acl website dstdomain .website.com
    http_access deny website blacklist
    http_access allow all
    ```   
3. Mettez en place des acls (http et localhost) squid qui interdisent le trafic HTTP en provenance de 127.0.0.1.
    ```
    acl localhost src 127.0.0.1/32
    acl http proto HTTP
    http_access deny localhost http
    http_access allow all
    ```   

4. Mettez en place une acl ho qui autorise l'accès au proxy tous les jours entre 8h et 17h uniquement
    ```
    acl ho time D 08:00-17h:00
    http_access allow ho
    http_access denied all
    ```   