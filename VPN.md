# Serveur VPN

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