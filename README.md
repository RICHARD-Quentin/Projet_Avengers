# Prérequis

Installer docker desktop https://www.docker.com/get-started et autoriser la virtualisation dans le BIOS si ce n'est pas deja le cas ( pour le vérifier, Gestionnaire des Tâches > Performance, en bas a droite en dessous des processeurs logiques, ça doit être Activé )

Installer gow https://github.com/bmatzelle/gow/releases

Bonus ( presque obligatoire ) installer le plug in Vue Devtools 
Chrome : https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd
Mozilla : https://addons.mozilla.org/fr/firefox/addon/vue-js-devtools/

# Comment lancer le projet ?

Etape 1 : cloner le projet ( evitez de cloner le projet dans un chemin avec des nom de dossier tout en majuscule )

git clone https://github.com/RICHARD-Quentin/Projet_Avengers.git

Etape 2 : lancer docker, attendre la notification "docker is running"

Etape 3 : lancer PHPStorm et se situer sur le dossier ou il y a le projet et le makefile dans la console de l'IDE
cd Projet_Avengers

Etape 4 : taper la commande make bash, normalement il y a ce genre de truc qui apparaît dans la console :

C:\Users\Quentin\PhpstormProjects\untitled>make bash
docker run --rm -it \
                -v C:/Users/Quentin/PhpstormProjects/untitled:/app \
                 -p 3001:3000 \
                 toroia/nodejs \
                 bash
bash-5.0#

Etape 4.5 : Installer yarn https://classic.yarnpkg.com/en/docs/install/#windows-stable

Etape 5 :toujours dans le terminal phpstorm se placer dans le projet : cd ProjetAvengers

Etape 6 :toujorus dans le terminal phpstorm taper la commande : yarn dev

Attendre que le projet compile, il devrait apparaître :

✔ Client
  Compiled successfully in 4.55s

✔ Server
  Compiled successfully in 4.32s
  
Etape 7 : localhost:3001 pour accéder au site

# Documentation
vueJS :
https://fr.vuejs.org/v2/guide/index.html#Rendu-declaratif

grafikart en a fait une bonne partie en vidéo : https://www.youtube.com/watch?v=g7YKecZhFRA&list=PLjwdMgw5TTLW-mAtlR46VajrKs4dep3y0


vuetify : https://vuetifyjs.com/fr-FR/getting-started/quick-start/

playlist de tuto vidéo vuetify en anglais : https://www.youtube.com/watch?v=2uZYKcKHgU0&list=PL4cUxeGkcC9g0MQZfHwKcuB0Yswgb3gA5
