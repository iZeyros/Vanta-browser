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
| Listes de filtres (`easylist.to`, `ublockorigin.github.io`, `easylist-downloads.adblockplus.org`, `raw.githubusercontent.com` pour la liste HaGeZi en protection renforcée et pour les scriptlets de uBlock Origin publiés avec Vanta ; en secours, si l'un d'eux ne répond pas : `cdn.jsdelivr.net`, `gitlab.com`) | Mettre à jour le bloqueur de pubs et de traqueurs (tous les 4 jours) | Une requête anonyme de téléchargement des listes | *Réglages › Bloqueur › Bloquer les pubs et les traqueurs* |
| Google / DuckDuckGo (icônes) | Afficher l'icône d'un site qui n'en fournit pas encore | Le **nom du site** (ex. `exemple.fr`), jamais l'adresse complète | *Réglages › Bloqueur & confidentialité › Icônes de sites en ligne* |
| GamerPower (`gamerpower.com`) | Lister les jeux gratuits sur la page d'accueil et, si tu actives l'alerte, vérifier toutes les 3 h s'il y en a de nouveaux | Une requête anonyme (la liste est gardée 1 h en cache) | *Réglages › Jeux gratuits* (accueil et alerte, l'alerte est désactivée par défaut) |
| Google Traduction | Traduire une page, **seulement quand tu cliques sur « Traduire »** | L'adresse de la page à traduire | Ne pas utiliser le bouton « Traduire » |
| Moteur de recherche choisi (Google, DuckDuckGo, Bing, Brave, Qwant) — **désactivé par défaut** | Suggestions de recherche dans la barre d'adresse, si tu actives l'option | Le texte que tu tapes dans la barre d'adresse (pas les adresses de sites, jamais en navigation privée) | *Réglages › Général › Suggestions du moteur de recherche* |
| Google (`clients2.google.com`) / Microsoft (`edge.microsoft.com`) | Télécharger une extension quand tu cliques sur « Ajouter à Vanta », puis vérifier une fois par jour si elle a une mise à jour | L'identifiant de l'extension et sa version, avec la version du moteur web | Ne pas installer d'extension depuis les magasins (ou la supprimer) |
| Réseau Tor (relais Tor, via Arti) — **seulement quand tu actives le VPN** | Cacher ton adresse IP aux sites : chaque connexion passe par trois relais Tor | Les relais reçoivent le trafic chiffré ; le relais de sortie voit le site contacté (le contenu reste chiffré en HTTPS), jamais ton adresse IP | Bouton VPN de la barre d'adresse (désactivé par défaut) |
| Microsoft SmartScreen | Vérifier la réputation des sites et des fichiers téléchargés | Les adresses visitées et les fichiers téléchargés, selon la politique de Microsoft | *Réglages › Bloqueur & confidentialité › Protection SmartScreen* |

Les pages que tu visites et les applications du panneau latéral (Discord, Spotify…)
reçoivent bien sûr ce que tout site reçoit d'un navigateur, selon leurs propres règles de
confidentialité. Le bloqueur intégré limite les traqueurs.
Quand le bloqueur est actif, Vanta indique aussi aux sites que tu refuses la vente et le partage
de tes données (signal Global Privacy Control : en-tête `Sec-GPC: 1` et `navigator.globalPrivacyControl`),
et les API publicitaires de Chromium (Topics, Protected Audience, Attribution Reporting, Shared Storage)
sont désactivées.

**VPN :** pour pouvoir l'activer et le couper instantanément, toutes les connexions de Vanta passent par un petit relais local (sur ton PC, `127.0.0.1`). VPN coupé, il se connecte directement aux sites, comme un navigateur normal ; VPN activé, il passe par Tor, sans jamais se replier en direct. Le réseau local (box, imprimantes…) reste toujours en direct. Pendant que le VPN est activé, WebRTC (appels audio et vidéo) est refusé, car il pourrait révéler ton adresse IP. L'annuaire des relais Tor est gardé dans `%APPDATA%\Vanta\tor` (démarrages plus rapides) ; rien d'autre n'est conservé.

**Bloc-notes :** tes notes sont enregistrées dans `%APPDATA%\Vanta\notes.json`, sur ton PC
uniquement, et ne sont jamais envoyées.

**Journal de diagnostic :** Vanta note les plantages et les erreurs dans `%APPDATA%\Vanta\logs`, sur
ton PC uniquement, sans les adresses visitées ni les noms de fichiers. Il n'est jamais envoyé : c'est
toi qui choisis de copier le rapport (*Réglages › Diagnostic*) pour le joindre à un ticket.

**Autorisations et zoom des sites :** tes choix (micro, caméra, position, notifications…) et le
zoom de chaque site sont enregistrés sur ton PC (`site_prefs.json`) ; tu peux les retirer dans
*Réglages › Autorisations des sites*.

**Navigation privée :** l'historique, les cookies et les données de sites de la fenêtre privée
sont effacés à sa fermeture, aucune icône n'est demandée en ligne, aucune suggestion de recherche
n'est envoyée et les autorisations accordées dans la fenêtre privée ne sont pas enregistrées.

**Moteur :** Vanta affiche les pages avec Microsoft Edge WebView2, un composant de Windows. Les
données de diagnostic éventuellement envoyées par ce composant dépendent des réglages de
confidentialité de Windows.

**Désinstallation :** le désinstalleur propose d'effacer toutes les données de Vanta.

Une question ? Ouvre un ticket sur [GitHub](https://github.com/iZeyros/Vanta-browser/issues).
