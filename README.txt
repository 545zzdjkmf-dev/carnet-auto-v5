CARNET AUTO — PWA de suivi des pleins (version 5) (version 2)
=====================================

CONTENU
- index.html : application complète
- manifest.json : configuration PWA
- sw.js : cache hors ligne
- icon-192.png et icon-512.png : icônes

FONCTIONS
- Gestion de plusieurs véhicules
- Enregistrement des pleins complets et partiels
- Historique avec kilométrage, litres, prix, montant et station
- Calcul de consommation entre pleins complets successifs, en tenant compte des pleins partiels intermédiaires
- Moyenne pondérée depuis le début du suivi
- Graphiques de consommation, dépenses mensuelles et prix au litre
- Export CSV compatible avec Excel, sauvegarde/restauration JSON
- Stockage local dans le navigateur
- Tableau de bord optimisé pour écran iPad/tablette, avec graphiques plus larges
- État de synchronisation explicite et guide de préparation CloudKit

INSTALLATION SUR IPHONE/IPAD (iOS/iPadOS 27)
1. Décompresser le ZIP sur un ordinateur.
2. Publier le contenu du dossier sur un hébergement HTTPS statique (par exemple GitHub Pages ou Netlify). Garder ensemble les 5 fichiers.
3. Ouvrir l'adresse HTTPS dans Safari sur l'iPhone/iPad.
4. Toucher Partager, puis « Ajouter à l'écran d'accueil ».
5. Activer « Ouvrir comme app web » si l'option apparaît, puis toucher Ajouter.

IMPORTANT
- Pour une vraie installation PWA et le fonctionnement hors ligne, l'application doit être servie en HTTPS (ou depuis localhost pour les tests). Ouvrir index.html directement depuis Fichiers ne suffit pas pour activer le service worker.
- Les données sont locales au navigateur/appareil et ne sont pas synchronisées entre iPhone et iPad. Exporter régulièrement une sauvegarde JSON.
- L'accès aux tarifs officiels ouvre le site gouvernemental. L'import automatique du flux live n'est pas activé dans cette version : le flux officiel est un fichier ZIP/XML et l'accès direct depuis une PWA peut être bloqué par CORS. Les prix saisis au plein restent disponibles sans connexion.
- La consommation affichée utilise les intervalles entre deux pleins complets successifs. Les litres de tous les pleins (y compris partiels) intermédiaires sont additionnés. Le premier plein complet sert de point de départ et ne crée pas de consommation avant qu'un plein complet suivant soit enregistré.
- Cette version est une première version autonome ; teste et exporte les données régulièrement avant d'y enregistrer un historique important.

SYNCHRONISATION ICLOUD / CLOUDKIT
La synchronisation multi-appareil n'est PAS encore active dans cette archive.
CloudKit JS nécessite un conteneur Apple, un schéma, une configuration Web et une authentification utilisateur. Ces éléments sont spécifiques au compte du propriétaire et ne peuvent pas être créés à sa place sans accès à son compte Apple Developer / CloudKit Console.
Ne place jamais une clé privée serveur dans le JavaScript client.
Documentation officielle : https://developer.apple.com/documentation/cloudkitjs
Console : https://icloud.developer.apple.com/

VERSION 3
- Ajout/modification/suppression de plusieurs véhicules, historique séparé
- Onglet France/Belgique de consultation Web des sources officielles
- France : prix des stations, via le site gouvernemental
- Belgique : prix maximaux du SPF Économie, pas prix de chaque station
- Pas de récupération automatique des tarifs dans l'interface (liens externes)
- La synchronisation iCloud reste à configurer et à développer ; les données restent locales

NOUVEAU — PRÉPARATION DE TRAJET
- Onglet « Trajet & autonomie » : saisie d'un départ, d'une destination et estimation de distance routière via les services publics OpenStreetMap/Nominatim et OSRM, si accessibles.
- Saisie manuelle de la distance possible si le service est indisponible.
- Estimation du carburant nécessaire, aller simple ou aller-retour.
- Estimation du carburant restant : capacité de réservoir configurée, kilomètres parcourus depuis le dernier plein complet et pleins partiels ajoutés ensuite.
- La consommation réelle moyenne est privilégiée ; sinon, la consommation théorique du véhicule est utilisée.
- Pour cette fonction, renseigner la capacité du réservoir et la consommation théorique dans la fiche du véhicule. Les données de trajet sont des estimations, pas une garantie d'autonomie.
- L'itinéraire automatique dépend d'API publiques externes, sans garantie de disponibilité. Vérifier la distance avec Plans/Google Maps.

MODIFICATION DES VEHICULES
Dans « Mes voitures », le bouton Modifier permet de compléter ou corriger le nom, l'immatriculation, le carburant, la capacité du réservoir et la consommation théorique.

NOUVEAU — PETROLIERS / ENSEIGNES
Sélection de TotalEnergies, Shell, Esso, BP, AVIA, Eni/Agip, Q8, Texaco, enseignes de grande distribution ou station indépendante. Le tableau de bord par véhicule totalise litres, euros et nombre de pleins par enseigne. L'enseigne est incluse dans l'export CSV. Les identifiants de marque sont affichés en badges textuels stylisés, pas en logos graphiques officiels.
