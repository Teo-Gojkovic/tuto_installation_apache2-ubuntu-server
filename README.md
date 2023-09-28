# Comment installer un serveur wab sur ubuntu server ([Apache2](https://doc.ubuntu-fr.org/apache2)) : 

Un serveur HTTP permet à un site web de communiquer avec un navigateur en utilisant le protocole HTTP(S) et ses extensions (WebDAV, etc.). Apache est probablement le serveur HTTP le plus populaire. C'est donc lui qui met à disposition la plupart des sites Web du WWW.
Il est produit par la Apache Software Foundation. C'est un logiciel libre fourni sous la licence spécifique Apache.

On utilise généralement Apache en conjonction avec d'autres logiciels, permettant d'interpréter du code et d'accéder à des bases de données. Le cas le plus courant est celui d'un serveur LAMP (Linux Apache MySQL PHP).

## Installation d'Apache2
Avant de commencer on va mettre notre OS à jour : 
```bash
apt-get update
```
```bash
apt install apache2 -y
```
*la condition `-y` est la pour éviter la confiramtion du téléchargement plus tard.*

### Votre serveur est prêt !
 
 **Si** vous ne connesez pas l'IP de la machine :
 ```bash
 ip a
 ```

Dans mon cas c'est 192.168.1.43 : 
![exemple](images/page.png)


## Comment modifier votre site : 
Dossier qui contiens les fichiers du site :
```bash
cd /var/www/html
```
Puis un `ls` pour voir les fichiers, et pour éditer on utilesera nano :
```bash
root@web-server-temp:~# cd /var/www/html
root@web-server-temp:/var/www/html# ls
index.html
root@web-server-temp:/var/www/html# nano index.html
```
![Alt text](images/cd.png)

Vous pouvez coder votre site depuis la console, mais c'est mieux d'importer vos fichier que vous avez coder depuis un IDE avec un logiciel de SFTP (SSH File Transfer Protocol).

Je conseille [WinSCP](https://winscp.net/eng/download.php), après les autres marche très bien comme [FileZilla](https://filezilla-project.org).

C'est des clients SFTP (SSH File Transfer Protocol) donc il faut autoriser le SSH via le port 22 si ce n'est pas déjà fait et vous connecter avec le compte root.

**SI** le SSH n'est pas autoriser : 
Pour télécharger SSH ou le mettre à jour :
```bash
apt install ssh -y
```
Autoriser le SSH
```bash
sudo nano /etc/ssh/sshd_config
```
décoomentez : 
```bash
port 22
PermitRootLogin yes
```
Exemple dans le dossier "exemple"

## **OPTIONEL** Ouvrir un port de votre routeur pour que le site soit consultable depuis l'exterieur : 

Changer le port  par défaut : 
```bash
sudo nano /etc/apache2/sites-available/000-default.conf
```
Et changer le port 80 en port de votre choix, le miens c'est 456.

On va maintenant ouvrir le port depuis Ubuntu Server : 
```bash
sudo ufw allow 456
```


### Sur le routeur
celon le routeur c'est une prosedure differente qu'il faudra effectuer, ici on va le faire sur une FreeBox.

Autres box/routeur : 
- [Orange](https://pratiquepc.fr/ouvrir-des-ports-sur-une-livebox/)
- [SFR](https://fluxdeconnaissances.com/information/page/read/40568-comment-ouvrir-les-ports-de-ma-sfr-box)
- [Bouygues](https://pratiquepc.fr/ouvrir-des-ports-sur-une-bbox/)
- [TP-Link](https://www.tp-link.com/fr/support/faq/134/#:~:text=Cliquez%20sur%20Avancé->%20NAT->%20Serveurs%20virtuels%20à%20gauche.&text=Tapez%20Nom%20%2C%20le%20port%20externe,interne%20et%20cliquez%20sur%20Activer%20.)
- [Ubiquiti](https://help.ui.com/hc/en-us/articles/235723207-UniFi-Gateway-Port-Forwarding)

Rendez vous sur le site de la box généralement le http://192.168.1.254
Allez dans `Paramètre de la box` puis dans le `mode avancé` ensuite `Gestion des ports` et pour finir `Ajouter une redirection`:

![Alt text](images/port-freebox.png)

