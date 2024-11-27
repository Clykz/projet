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

````
[dylan@localhost ~]$ sudo firewall-cmd --zone=public --permanent --add-service=http
success
[dylan@localhost ~]$ sudo firewall-cmd --reload
success
````