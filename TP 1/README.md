# TP 1

# Etape 1 : Installation et configuration d’un serveur we
#### Il faut d'abord installer Apache sur l'appareil, pour cela tapper 'Apache download' sur un navigateur et procéder a l'installation.
#### Dans le gestionnaire de fichier, clic droit sur le dossier puis cliquer sur "ouvrir dans un terminal".
#### Une fois dans le terminal, effectuer ces commandes :
- `sudo apt update`
- `sudo apt install build-essential libpcre3 libpcre3-dev libssl-dev`
- `./configure`
- `make` **(sa peut prendre du temps)**
- `sudo make install`

  ## Félicitation, vous avez installer Apache sur votre machine

  ### Maintenant, on vérifie le statue

  #### Dans le terminal tapper `ps aux | grep httpd`
  ### Si vous voyez écrit HTTPD sur plusieurs ligne, sa fonctionne mais pour en être certain :
  #### Ouvrez un navigateur et écriver `http://localhost`
  ### Si une page s'ouvre et écrit : **It Works!** alors Apache fonctionne bien sur votre appareils.

  ## Pour configurer le serveur
  ### tapper la commande
  `nano index.html`
  ### Ensuite rentrez ce code :
```html
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
```
##### Le rendu obtenu :
<img width="889" height="859" alt="image" src="https://github.com/user-attachments/assets/6dcf15b2-997c-4223-9682-10dacd1dbf6a" />

### Ensuite :
- CTRL + O puis ENTREE pour sauvegarder
- CTRL + X pour quitter le nano

### Vous devez maintenant ouvrir votre navigateur et lancer l'adresse suivant
- `http://localhost`
#### Vous devez obtenir ce résultat 

<img width="886" height="915" alt="image" src="https://github.com/user-attachments/assets/249b50d5-e281-407c-a697-2cdd123865ac" />

## Si tous fonctionne correctement
### On va modifier la configuration pour que le serveur réponde sur un port non standard
- `sudo nano /usr/local/apache2/conf/httpd.conf`
#### Chercher la ligne "Listen 80" <img width="103" height="19" alt="image" src="https://github.com/user-attachments/assets/fe756301-feba-4ed1-a611-9ca2e1a93e61" />
### Modifier la ligne pour la transformer en "***Listen 8080***"
- CTRL + O  puis ENTREE pour sauvegarder
- CTRL + X pour quitter le nano
### Il faut redémarrer le système sudo avec la commande `sudo /usr/local/apache2/bin/apachectl restart`
### Vous pouvez lancer l'adresse "http://localhost:8080` sur votre navigateur

# Etape 2 : Configuration du pare-feu avec  UFW
