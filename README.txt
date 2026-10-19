CARNET AUTO V6 — correction + synchronisation Firebase

CONTENU
- index.html : application corrigée, sélecteur de pétrolier, synchronisation Firebase Auth + Cloud Firestore
- manifest.json, sw.js et icônes : installation PWA
- firestore.rules : règles de sécurité à publier dans Firebase

ETAPE 1 — METTRE A JOUR GITHUB
Dans le dépôt GitHub car​net-auto-v5, ouvrir Add file > Upload files et déposer TOUS les fichiers de cette archive (index.html, manifest.json, sw.js, icon-192.png, icon-512.png). Valider avec Commit changes. Attendre le redéploiement GitHub Pages puis recharger le site.

ETAPE 2 — ACTIVER L'AUTHENTIFICATION
Dans Firebase Console > Authentication > Sign-in method, activer « E-mail / mot de passe ».

ETAPE 3 — ENREGISTRER L'APPLICATION WEB
Dans Firebase Console > Paramètres du projet (roue dentée) > Général > Vos applications, ajouter une application Web (icône </>) si elle n'existe pas déjà. Copier les champs apiKey, authDomain, projectId et appId.
Dans Carnet Auto > Export & sauvegarde > Synchronisation entre appareils, coller ces quatre valeurs puis cliquer « Enregistrer la configuration Firebase ».
La configuration Web n'est pas une clé privée. Ne jamais copier de clé privée ou de compte de service dans le navigateur.

ETAPE 4 — SECURISER FIRESTORE
Firebase Console > Firestore Database > Règles. Remplacer les règles par le contenu de firestore.rules puis cliquer Publier.
Ces règles autorisent uniquement un utilisateur connecté à lire/écrire sous son propre identifiant. Ne pas activer des règles publiques allow read, write: if true.

ETAPE 5 — CREER LE COMPTE ET SYNCHRONISER
Dans l'application, saisir une adresse e-mail et un mot de passe d'au moins 6 caractères puis cliquer « Créer un compte ». Sur les autres appareils, ouvrir la même URL et se connecter avec ce même compte.
Au premier appareil, si Firestore ne contient pas encore de sauvegarde, l'application y copie les données locales. Sur les autres appareils, la sauvegarde cloud existante est chargée.

IMPORTANT
- La synchronisation Firebase est ajoutée au code, mais ne fonctionnera qu'après les étapes de configuration ci-dessus.
- Avant de démarrer, utiliser « Sauvegarde complète » pour télécharger un JSON de sécurité.
- Les données sont stockées dans un document par compte. Pour l'instant, les mises à jour sont synchronisées à l'enregistrement; ce n'est pas une fusion intelligente des modifications simultanées sur deux appareils. Éviter de modifier les données sur plusieurs appareils exactement au même moment.
- Les prix des stations ne sont pas importés automatiquement; les liens officiels restent accessibles dans l'onglet Prix France / Belgique.
