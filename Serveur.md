# Serveur WEB 

- **Installation Apache2**
````
sudo dnf install httpd
````
- **Demarrage Apache**
````
sudo systemctl start http
````
- **Status Apache**
````
[dylan@localhost ~]$ sudo systemctl status httpd
● httpd.service - The Apache HTTP Server
     Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; preset: disabled)
     Active: active (running) since Wed 2024-11-27 16:34:27 CET; 54s ago
       Docs: man:httpd.service(8)
   Main PID: 52051 (httpd)
     Status: "Total requests: 0; Idle/Busy workers 100/0;Requests/sec: 0; Bytes served/sec:   0 B/sec"
      Tasks: 177 (limit: 4671)
     Memory: 21.8M
        CPU: 54ms
     CGroup: /system.slice/httpd.service
             ├─52051 /usr/sbin/httpd -DFOREGROUND
             ├─52052 /usr/sbin/httpd -DFOREGROUND
             ├─52053 /usr/sbin/httpd -DFOREGROUND
             ├─52054 /usr/sbin/httpd -DFOREGROUND
             └─52055 /usr/sbin/httpd -DFOREGROUND

Nov 27 16:34:27 localhost.localdomain systemd[1]: Starting The Apache HTTP Server...
Nov 27 16:34:27 localhost.localdomain httpd[52051]: AH00558: httpd: Could not reliably determine the server's fully qua>
Nov 27 16:34:27 localhost.localdomain systemd[1]: Started The Apache HTTP Server.
Nov 27 16:34:27 localhost.localdomain httpd[52051]: Server configured, listening on: port 80
lines 1-20/20 (END)
````
- **Configuration serveur**
````
sudo nano /var/www/html/index.html
````
````
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Linux is Better</title>
    <style>
        body {
            background-color: #f0f0f0;
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: Arial, sans-serif;
        }
        h1 {
            color: #333;
            font-size: 48px;
            text-align: center;
            animation: fadeIn 2s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
    </style>
</head>
<body>
    <h1>Linux is better</h1>
</body>
</html>
````

````
sudo firewall-cmd --zone=public --permanent --add-service=http
````
````
sudo firewall-cmd --reload
````
- **Accès page web**
````
http://IP_du_site
````
## Configuration parefeu firewalld

- **Active le parefeu**
```
sudo systemctl start firewall
sudo firewall-cmd --reload
```
- **Ajouter des services**
```
sudo firewall-cmd --zone=public --add-service=http --permanent
sudo firewall-cmd --zone=public --add-service=https --permanent
sudo firewall-cmd --reload
```
- **Vérifie la modification**
```
firewall-cmd --zone=public --list-all
```
- **Ouverture des ports dans la zone public**
```
sudo firewall-cmd --zone=public --permanent --add-port=443/tcp
sudo firewall-cmd --zone=public --permanent --add-port=80/tcp
sudo firewall-cmd --reload
```
- **Retire les services par defaut**
```
sudo firewall-cmd --permanent --remove-service dhcpv6-client
sudo firewall-cmd --permanent --remove-service cockpit
sudo firewall-cmd --reload
````