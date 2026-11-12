# SCÈNE — prototype Chromebook

Cette version est une application web installable (PWA) pensée pour ChromeOS et Google Chrome. Elle ne nécessite pas Windows ni une connexion Internet permanente après son installation initiale et la mise en cache.

## Fonctions du prototype
- Import de fichiers audio depuis le Chromebook, stockés localement dans IndexedDB.
- Bibliothèque, recherche et marquage de sons comme effets.
- Liste de lecture, réorganisation manuelle.
- GO / piste suivante, lecture automatique en option.
- Fondu enchaîné réglable (0 à 15 secondes, valeur initiale 5 s).
- Soundboard avec plusieurs effets simultanés.
- Volume master, pause, stop et PANIC.
- Mise en cache des fichiers de l'application pour un usage hors ligne.

## Démarrer sur Chromebook

Pour des raisons de sécurité, Chrome n'autorise pas toutes les fonctions (IndexedDB, service worker et installation PWA) depuis un simple fichier `file://`. Il faut servir le dossier en HTTPS ou depuis localhost.

### Méthode simple : hébergement statique HTTPS
1. Décompressez le ZIP sur un ordinateur ou dans votre espace de travail.
2. Publiez le contenu du dossier sur un hébergement statique HTTPS (par exemple GitHub Pages).
3. Ouvrez l'adresse HTTPS dans Chrome sur le Chromebook.
4. Attendez le chargement complet une première fois. Utilisez « Installer l’application » si Chrome le propose, ou le menu Chrome > Installer la page.
5. Importez les fichiers audio. Ils restent dans le stockage local du navigateur sur ce Chromebook.

Ne mettez pas vos fichiers audio personnels dans un dépôt public. Seuls les fichiers de l'application doivent être hébergés.

### Test local
Si l'environnement Linux est activé sur le Chromebook, installez Python 3 puis, dans le dossier du projet, lancez :
`python3 -m http.server 8000`
Ouvrez ensuite `http://localhost:8000` dans Chrome. Le service worker peut être limité sur localhost selon le navigateur; HTTPS est préférable pour tester l'installation PWA.

## Compatibilité et limites à connaître
- Cible : Chromebook récent avec Google Chrome à jour et stockage local autorisé.
- La lecture utilise Web Audio API et les formats décodables par le navigateur. MP3 et WAV sont généralement les plus sûrs. Certains FLAC, AAC/M4A ou autres codecs dépendent de la version de ChromeOS et du codec embarqué.
- Les fichiers sont stockés dans le profil Chrome de cet appareil. Ils ne sont pas synchronisés automatiquement entre appareils et peuvent être effacés si les données du site sont supprimées.
- Les fichiers audio importés ne sont pas inclus dans le cache hors ligne du site : ils sont stockés séparément dans IndexedDB.
- Les longs fichiers audio sont décodés en mémoire pour la lecture et les fondus. De très gros fichiers ou de nombreux effets simultanés peuvent dépasser la mémoire disponible sur certains Chromebooks.
- La sortie est la sortie audio par défaut de ChromeOS. Ce prototype ne gère pas encore la sélection de périphériques, les sorties multiples, MIDI, les raccourcis clavier dédiés ni un mode de secours matériel.
- Le prototype n'est pas encore validé pour une représentation publique. Faites des essais avec le matériel réel, les fichiers du spectacle et les conditions de charge avant toute utilisation en régie.

## Important
Cette livraison est un prototype fonctionnel de départ, pas un logiciel de régie certifié ou garanti sans interruption. La compatibilité exacte dépend du modèle de Chromebook, de la version de ChromeOS et des formats audio utilisés.
