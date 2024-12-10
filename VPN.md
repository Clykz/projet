

Insatallation de wireguard :
````
sudo dnf install -y epel-release
sudo dnf install -y wireguard-tools -y
````

génération de la clé:

````
wg genkey | sudo tee /etc/wireguard/wg0.priv | wg pubkey | sudo tee /etc/wireguard/wg0.pub
````