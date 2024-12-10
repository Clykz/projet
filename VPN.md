# Serveur VPN

- **configurer l'interface réseaux**
````
sudo cat /etc/sysconfig/network-scripts/ifcfg-enp0s3

DEVICE=enp0s3
NAME=lan1

ONBOOT=yes
BOOTPROTO=static

IPADDR=10.7.1.111
NETMASK=255.255.255.0
GATEWAY=10.7.1.254
DNS1=1.1.1.1
````

- **appliquer la configuration**
````
udo nmcli connection reload
sudo nmcli connection up lan1
````


- **Insatallation de wireguard**
````
sudo dnf install -y epel-release
sudo dnf install -y wireguard-tools -y
````

- **génération de la clé**

````
wg genkey | sudo tee /etc/wireguard/wg0.priv | wg pubkey | sudo tee /etc/wireguard/wg0.pub
````

- **Ecrire le fichier de configuration du serveur**
````
 sudo nano /etc/wireguard/wg0.conf

 [Interface]
PrivateKey =  YHxBnZoB1sukLnj8LfQIwC90hLCqIFDIyj03x+BhblA=
Address = 10.7.200.1/24
ListenPort = 51820
````

- **Démarrez l'interface réseau wg0**
````
sudo systemctl start wg-quick@wg0
````

- **activation du routage**
````
sudo sysctl -w net.ipv4.ip_forward=1
sudo sysctl -w net.ipv6.conf.all.forwarding=1
sudo firewall-cmd --add-interface=wg0 --zone=public --permanent
sudo firewall-cmd --add-masquerade --permanent
sudo firewall-cmd --reload
````

- **partie suivante à faire sur le client**


- **Modifier le fichier de configuration du serveur**
````
sudo nano /etc/wireguard/wg0.conf

[Interface]
PrivateKey = <CLE_PRIVEE_DU_SERVEUR>
Address = 10.7.200.1/24
ListenPort = 51820


[Peer]
PublicKey = <CLE_PUBLIQUE_DU_CLIENT>
AllowedIps = 10.7.200.11/32
````

- **Redémarrer l'interface du serveur après l'ajout du client**
````
sudo systemctl restart wg-quick@wg0
````

- **Vérifier qu'on voit bien un nouveau client**
````
sudo wg show
````

- **connecter le serveur web au vpn**
````

````