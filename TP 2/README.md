# TP 2

# 1. Préparation et configuration du webhook

## Pour créer un webhook sur discord il faut créer un salon sur un serveur discord, je les appeler "#alertes-securite"
## Ensuite on va dans les paramètres du salon puis on clique sur intégration et ensuite sur Webhooks 
<img width="1302" height="991" alt="image" src="https://github.com/user-attachments/assets/ceeb14cc-b8d7-4543-b182-2ffe2e76d6fd" />

## On clique sur le webhook qui viens de se créer automatiquement puis on fait "copier l'URL du webhook"
<img width="802" height="537" alt="image" src="https://github.com/user-attachments/assets/d7791244-8f55-471a-9b8b-d3ea0c904ebf" />

## Et j'ai ensuite coller l'URL dans le salon pour le conserver
### _Mon URL est :_ https://discord.com/api/webhooks/1436027350981541920/h23Gh6MDhE961-iN3XBDPpYOjG96jMWdJmzIjXP_pRagHDj1ygFjUvHrFVhdl3wSwumG

# 2. Surveillance des accès à des fichiers sensibles

## J'ai installer inotify tools en fesant : 
- `sudo apt update`
- `sudo apt install inotify-tools`

## Ensuite comme je n'est pas trouver de fichier secret.txt sur ma vm j'en est créer un avec `sudo touch /etc/secret.txt`

## Et j'ai fait ```nano surveillance_fichier.sh```
## J'ai écrit :
```
#!/bin/bash
FILE_TO_WATCH="/etc/secret.txt"
WEBHOOK_URL="https://discord.com/api/webhooks/1436027350981541920/h23Gh6MDhE961-iN3XBDPpYOjG96jMWdJmzIjXP_pRagHDj1ygFjUvHrFVhdl3wSwumG"
while inotifywait -e open "$FILE_TO_WATCH"; do
  curl -H "Content-Type: application/json" -X POST \
    -d "{\"content\": \"🚨 Accès détecté au fichier secret: $FILE_TO_WATCH\"}" \
    $WEBHOOK_URL
done
```
## Et j'ai fait :
- ```chmod +x surveillance_fichier.sh```
- ```nohup ./surveillance_fichier.sh &```
### Ce qui a rendu le nano executable et la lancer en tache de fond

# 3. Surveillance des connexions SSH hors des horaires de bureau

## J'ai fait `nano surveillance_ssh.sh`
## J'ai écrit sa avant de sauvegarder et quitter le nano :
```
#!/bin/bash
FILE_TO_WATCH="/etc/secret.txt"
WEBHOOK_URL="[https://discord.com/api/webhooks/TON_WEBHOOK](https://discord.com/api/webhooks/1436027350981541920/h23Gh6MDhE961-iN3XBDPpYOjG96jMWdJmzIjXP_pRagHDj1ygFjUvHrFVhdl3wSwumG)"
while inotifywait -e open "$FILE_TO_WATCH"; do
  curl -H "Content-Type: application/json" -X POST \
    -d "{\"content\": \"🚨 Accès détecté au fichier secret: $FILE_TO_WATCH\"}" \
    $WEBHOOK_URL
done
```

## Je les rendu éxecutable avec ```chmod +x surveillance_ssh.sh```
## Puis j'ai lancer le script en tâche de fond avec ``nohup ./surveillance_ssh.sh &``
## Pour que surveillance_ssh se lance toute les 5 minutes j'ai fait ```crontab -e```
## Et j'ai rajouter la ligne :
```
*/5 * * * * /chemin/vers/surveillance_ssh.sh
```
# Test

## J'ai voulu tester si j'avais bien le message qui s'envoie sur discord 
## Donc j'ai relancer le script de surveillance_fichier.sh en fesant ```nohup ./surveillance_fichier.sh &```
## Puis j'ai fait un `cat /etc/secret.txt`
## Et j'ai bien reçu le message sur le salon discord
<img width="621" height="622" alt="image" src="https://github.com/user-attachments/assets/38aa3e00-f776-4092-8a15-cbd9e25776bf" />

#### ( Là j'avais un peu trop spam la commande )
