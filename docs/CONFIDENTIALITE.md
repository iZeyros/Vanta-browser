# Politique de confidentialité de Vanta

*Dernière mise à jour : novembre 2026*

Vanta est un navigateur **sans compte et sans télémétrie** : il n'envoie aucune statistique
d'utilisation, aucun identifiant et aucune donnée de navigation à ses auteurs. Tes données
(favoris, historique, réglages, mots de passe enregistrés, téléchargements) restent **uniquement
sur ton PC**, dans `%APPDATA%\Vanta`.

Pour fonctionner, Vanta contacte quelques services. Voici la liste complète, et comment
désactiver chacun d'eux.

| Service | Pourquoi | Ce qui est envoyé | Désactiver |
|---|---|---|---|
| GitHub (`api.github.com`, `github.com`) | Vérifier et télécharger les mises à jour (au démarrage puis toutes les 6 h) | Une requête anonyme vers la page des versions de Vanta | *Réglages › Mises à jour › Ne jamais vérifier* |
| Listes de filtres (`easylist.to`, `ublockorigin.github.io`, `easylist-downloads.adblockplus.org`) | Mettre à jour le bloqueur de pubs et de traqueurs (tous les 4 jours) | Une requête anonyme de téléchargement des listes | *Réglages › Bloqueur › Bloquer les pubs et les traqueurs* |
| Google / DuckDuckGo (icônes) | Afficher l'icône d'un site qui n'en fournit pas encore | Le **nom du site** (ex. `exemple.fr`), jamais l'adresse complète | *Réglages › Bloqueur & confidentialité › Icônes de sites en ligne* |
| GamerPower (`gamerpower.com`) | Lister les jeux gratuits sur la page d'accueil | Une requête anonyme | *Réglages › Bloqueur & confidentialité › Jeux gratuits sur l'accueil* |
| Google Traduction | Traduire une page, **seulement quand tu cliques sur « Traduire »** | L'adresse de la page à traduire | Ne pas utiliser le bouton « Traduire » |
| Microsoft SmartScreen | Vérifier la réputation des sites et des fichiers téléchargés | Les adresses visitées et les fichiers téléchargés, selon la politique de Microsoft | *Réglages › Bloqueur & confidentialité › Protection SmartScreen* |

Les pages que tu visites et les applications du panneau latéral (Discord, Spotify…)
reçoivent bien sûr ce que tout site reçoit d'un navigateur, selon leurs propres règles de
confidentialité. Le bloqueur intégré limite les traqueurs.

**Navigation privée :** l'historique, les cookies et les données de sites de la fenêtre privée
sont effacés à sa fermeture, et aucune icône n'est demandée en ligne.

**Moteur :** Vanta affiche les pages avec Microsoft Edge WebView2, un composant de Windows. Les
données de diagnostic éventuellement envoyées par ce composant dépendent des réglages de
confidentialité de Windows.

**Désinstallation :** le désinstalleur propose d'effacer toutes les données de Vanta.

Une question ? Ouvre un ticket sur [GitHub](https://github.com/iZeyros/Vanta-browser/issues).
