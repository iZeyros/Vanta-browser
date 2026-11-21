# Vanta — documentation développeur

> Présentation et téléchargement : voir le [README](../README.md).

Navigateur Windows pensé pour les joueurs, écrit en Rust avec **WebView2** (le moteur Chromium
d'Edge déjà installé sur Windows 10/11). L'interface est en HTML/CSS dans une WebView dédiée,
toute la logique (onglets, limiteurs, bloqueur, stockage) est en Rust.

## Compiler et lancer

```powershell
cd "D:\Documents(D)\Browser"
cargo run --release
```

Prérequis : Rust (toolchain MSVC) + Visual Studio Build Tools, et le runtime WebView2 Evergreen
(présent par défaut sur Windows 10/11). Le premier build prend quelques minutes (SQLite, adblock).
L'exécutable final est `target\release\vanta.exe`.

## Créer l'installateur

```powershell
.\build-installer.ps1
```

Compile Vanta puis l'installateur et produit `dist\VantaSetup.exe` (un seul fichier, qui
embarque Vanta). L'installateur permet de choisir **n'importe quel dossier** (un
sous-dossier `Vanta` est ajouté si besoin ; il demande les droits administrateur seulement
pour un dossier protégé comme `C:\Program Files`), crée les raccourcis Bureau / menu
Démarrer, peut activer le lancement au démarrage de Windows, et inscrit Vanta dans
*Paramètres > Applications* avec un désinstalleur (`uninstall.exe`) qui propose de garder
ou supprimer les données. Relancé sur une installation existante, il fait une mise à jour.

## Mises à jour automatiques

Les versions sont publiées sur **GitHub Releases**. Vanta vérifie au démarrage puis toutes
les 6 h, télécharge la nouvelle version en arrière-plan, vérifie sa **signature Ed25519**,
puis propose « Redémarrer » (ou l'installe à la fermeture). Réglable dans
*Réglages > Mises à jour* : télécharger puis proposer (défaut), installer automatiquement,
prévenir seulement, ou jamais. L'installateur télécharge lui aussi la dernière version
(repli sur la version incluse s'il est hors ligne).

### Mise en place (une seule fois)

1. Crée un dépôt GitHub **public** (ex. `vanta`) et indique-le dans `release.json` :
   `"github_repo": "ton-pseudo/vanta"`.
2. Installe GitHub CLI : `winget install GitHub.cli`, puis `gh auth login`.

### Publier une version

```powershell
.\publish-release.ps1 -Version 0.2.0 -Notes "Nouveautés…"
```

Le script met à jour le numéro de version, compile, **signe** `vanta.exe`, compile
l'installateur et publie la release (`vanta.exe`, `vanta.exe.sig`, `VantaSetup.exe`).
Avec `-Store`, il crée aussi le paquet Microsoft Store (`dist\Vanta-<version>.msix`, signé par
Microsoft après envoi dans le Partner Center). Voir [SIGNATURE.md](SIGNATURE.md).
Lien permanent vers le dernier installateur :
`https://github.com/<pseudo>/vanta/releases/latest/download/VantaSetup.exe`.

Au premier lancement, il crée la clé de signature : privée dans
`%APPDATA%\VantaRelease\signing.key` (**à sauvegarder**, jamais dans le dépôt), publique
dans `assets\update-public.key` (à garder dans le dépôt). Sans la clé privée, plus aucune
mise à jour ne sera acceptée par les installations existantes.

> Les versions compilées **avant** la configuration (sans `release.json` ni clé) ne se
> mettent pas à jour : réinstalle une fois avec un `VantaSetup.exe` publié.

## Fonctionnalités V1

| Domaine | Détail |
|---|---|
| **Vanta Core** | Limiteur **RAM** (suspension puis déchargement des onglets les plus anciens), plafond **CPU** strict (Job Object Windows), limiteur **réseau** par onglet (DevTools Protocol), suspension auto des onglets inactifs, graphiques en direct |
| **Mode jeu** | Détection auto d'un jeu plein écran (exclusif ou fenêtré sans bordure) → limites renforcées + suspension des onglets d'arrière-plan. Modes Auto / Forcé / Off |
| **Bloqueur** | adblock-rust (moteur de Brave) avec EasyList, EasyPrivacy, uBlock filters et Liste FR, masquage cosmétique, liste blanche par site (clic sur le bouclier) |
| **Panneau latéral** | Discord, YouTube Music, Spotify (sessions conservées, la musique continue en arrière-plan) + apps perso dans les réglages. Chaque appli s'affiche en **version mobile portrait** (émulation téléphone) ou bureau, avec zoom, largeur réglable (glisser le bord) et ouverture en onglet |
| **Onglets** | Session restaurée en **chargement paresseux**, réordonnancement par glisser, muet, dupliquer, décharger, rouvrir (Ctrl+Maj+T), clic molette pour fermer |
| **Écran partagé** | Bouton dans la barre d'outils ou **Ctrl+clic** sur un onglet |
| **Hub gaming** | Page d'accueil avec jeux gratuits (Epic, Steam, GOG, Prime, itch.io via GamerPower), sites favoris, statistiques |
| **Import** | Favoris + historique depuis Chrome, Edge, Brave, Opera, Opera GX |
| **Extensions** | Extensions Chrome décompressées (dossier `%APPDATA%\Vanta\extensions`) |
| **Favoris** | Gestionnaire vanta://bookmarks : dossiers et sous-dossiers, renommage (F2 / double-clic), glisser-déposer (favoris et dossiers), sélection multiple (Ctrl/Maj), déplacement groupé, annulation de suppression ; dossiers affichés dans la barre de favoris |
| **Téléchargements** | Gestion native WebView2 (téléchargement parallèle activé), menu déroulant sous le bouton ↓ avec progression, taille, vitesse et temps restant, pause / reprise / annulation / réessai, double-clic pour ouvrir ou exécuter, anneau de progression sur le bouton |
| **Démarrage** | Option « Lancer Vanta au démarrage de Windows » (clé `Run` de l'utilisateur) et « Démarrer réduit » |
| **Navigation privée** | Fenêtre privée (Ctrl+Maj+N, bouton masque de la barre latérale, action d'onglet, clic droit sur un lien) : processus séparé en mode InPrivate, rien n'est conservé à la fermeture (historique, cookies, cache, session, liste des téléchargements, icônes) ; thème violet et badge PRIVÉ |
| **VPN (Tor)** | `src/tor.rs` : relais SOCKS5 local (127.0.0.1, port au hasard) toujours actif, donné à WebView2 (`--proxy-server`, réseau local en direct) et à ureq (`ALL_PROXY=socks5h://…`) ; VPN coupé = connexion directe (Happy Eyeballs simplifié), activé = Arti (Tor en Rust, lancé au 1er usage), jamais de repli en direct ; chaque bascule coupe les connexions ouvertes (`watch` de génération). WebRTC refusé pendant le VPN : garde injectée dans toutes les pages (`webrtc_guard_js`, fonction secrète par session appelée à chaque bascule). Bouton `#vpn` à côté du bouclier, menu `vpn` du flyout (interrupteur, progression, « Nouvelle identité » = `isolated_client`), Ctrl+Maj+E ; `Settings.vpn` retenu (pas en privé) |
| **Lecteur réduit** | Bouton « Lecteur réduit » au survol des vidéos et dans la barre d'outils : picture-in-picture natif de Chromium (geste utilisateur via DevTools `Runtime.evaluate`), repli sur une fenêtre Vanta toujours au premier plan (WebView de l'onglet déplacée avec `reparent`) ; option automatique au changement d'onglet |
| **Sites fréquents** | Retirables depuis l'accueil (×, annulable) : `hidden_sites.json`, l'historique n'est pas modifié |
| **Divers** | Historique SQLite, téléchargements, plein écran vidéo, DevTools (F12), couleur d'accent |

## Raccourcis

`Ctrl+T` nouvel onglet · `Ctrl+W` fermer · `Ctrl+Maj+T` rouvrir · `Ctrl+Tab` / `Ctrl+Maj+Tab` changer ·
`Ctrl+L` / `F6` barre d'adresse · `Alt+Entrée` (dans la barre) ouvrir dans un nouvel onglet ·
`Ctrl+D` favori · `Ctrl+H` historique · `Ctrl+J` téléchargements · `F12` DevTools ·
clic droit sur un onglet : actions (dupliquer, écran partagé, son, décharger, fermer).

## Architecture

```
src/
  main.rs        point d'entrée
  storage.rs     paramètres, favoris, session, téléchargements, réglages par site (JSON)
                 + historique (SQLite)
  suggest.rs     suggestions du moteur de recherche (option, désactivée par défaut)
  crx.rs         extensions des magasins : adresse de téléchargement, vérification CRX3
                 (signature RSA du développeur), décompression ZIP sûre, autorisations en clair
  diag.rs        journal de diagnostic local (logs\vanta.log, panique, rapport)
  extinfo.rs     manifestes des extensions (nom traduit, popup, options, identifiant)
  security.rs    règles de sécurité testables partout : origine des pages internes, fenêtres
                 ouvertes par les sites, schémas externes bloqués, téléchargements à risque
  blocker.rs     listes de filtres, 2 moteurs adblock-rust (pubs / traqueurs EasyPrivacy)
  import.rs      import Chromium (Bookmarks JSON, History SQLite)
  blocker.rs     (détail) 2 moteurs adblock (pubs + cosmétique / traqueurs) + table compacte de
                 domaines HaGeZi Pro (protection renforcée, ~5 Mo) + règles VANTA_STRONG / VANTA_MAX
                 (niveaux renforcé / maximal, `$third-party`) dans le moteur traqueurs ; requête bloquée = adresse
                 détournée vers https://0.0.0.0:1/ (échec réseau immédiat), 403 vide pour cadres
                 et images (repliés dans la page), ressource de remplacement servie en 200 pour
                 les règles `$redirect=` ; masquage générique : COSMETIC_JS (pages.rs) signale les classes / id,
                 commande web « cosm » -> hidden_class_id_selectors ; scriptlets (`##+js(...)`) :
                 ressources de uBlock Origin (docs/ubo/resources.json, GPLv3, téléchargées comme
                 les listes, listes uBO « de confiance » pour les `trusted-*`), précédées de la
                 garde MIT `src/adguard.js` (API du lecteur YouTube nettoyée, pubs YouTube passées,
                 cadres bloqués repliés, Global Privacy Control, anti-empreinte canvas / WebGL /
                 audio avec une graine tirée à chaque lancement : `blocker::set_farbling`) ; `scriptlets_for(url)` en cache
                 par nom d'hôte, ajoutés par onglet en script de document (native.rs
                 `prepare_scriptlets`, au plus 64 sites, retirés quand les listes changent)
  games.rs       flux des jeux gratuits (GamerPower, cache 1 h) + tri des nouveaux pour l'alerte
  wishlist.rs    liste de souhaits (wishlist.json, 100 jeux) et prix CheapShark (recherche, 25 jeux par
                 requête, cache 1 h, noms des boutiques 7 j) ; `alert_for` : seuil, plus bas historique, une
                 alerte par offre ; liens = page de redirection CheapShark (condition de son API)
  theme.rs       thèmes complets (palettes) servis en vanta://theme.css
  i18n.rs        langue (fr / en / celle de Windows) ; dictionnaire ui/i18n-en.json servi avec le
                 traducteur ui/i18n.js en vanta://i18n.js, et tr() pour les textes natifs
  notes.rs       bloc-notes du panneau latéral (notes.json, limites)
  sysmon.rs      RAM (mémoire privée) / CPU de Vanta + ses processus WebView2
  win/mod.rs     fenêtre tao, WebView enfants, IPC, politique mémoire, limiteurs
  win/native.rs  COM WebView2 (requêtes, CDP, suspension, audio, extensions, plantages,
                 zoom, autorisations), Job Object CPU, détection de jeu plein écran
  win/omni.rs    suggestions de la barre d'adresse (onglets, favoris, historique, complétion)
  win/site.rs    zoom mémorisé par site, demandes d'autorisation (bulle) et menu du cadenas
  win/crash.rs   récupération après plantage (rechargement, page « Oups », redémarrage)
  win/extensions.rs  bouton Extensions : liste et popup d'extension sous le bouton
  win/pages.rs   pages internes vanta:// embarquées + script injecté dans les onglets
  win/notify.rs  notifications : modèle unique, centre (cloche), actions gardées côté Rust
  win/groups.rs  groupes d'onglets (couleurs, onglets toujours côte à côte)
  win/gamealert.rs  alerte jeux gratuits (question unique, vérification toutes les 3 h)
  win/pricealert.rs commandes `wish_*` de l'accueil, alerte de prix (toutes les 6 h, 1re après 90 s)
  win/tip.rs     infobulles de l'interface (petite fenêtre flottante sans focus ni clics)
  favicons.rs    cache des icônes de sites
ui/              interface (chrome.html), pages internes (start, settings, history…),
                 menu déroulant (flyout.html : téléchargements, bouclier, notifications,
                 dossiers de favoris en cascade, recherche d'onglets, suggestions de la barre
                 d'adresse, autorisations, cadenas), pile de notifications
                 (notify.html), mode lecture (reader.html), listes déroulantes arrondies (select.js)
ui/vendor/       Readability.js (Mozilla, licence Apache 2.0) pour le mode lecture
assets/          icône de l'application (vanta.ico, app-icon.svg)
installer/       VantaSetup : installateur / désinstalleur (Rust + WebView2)
crates/vanta-update/  mises à jour : GitHub Releases, téléchargement, signature Ed25519
tools/release/   vanta-release : clé de signature + signature des versions
release.json     dépôt GitHub des mises à jour
```

Le menu déroulant et les notifications sont des **fenêtres flottantes transparentes**
rattachées à la fenêtre principale : la page dessine elle-même les coins arrondis et
l'ombre, et le menu peut déborder de la fenêtre (sous-menus des dossiers).

Toutes les WebView partagent **un seul environnement WebView2** (mêmes processus navigateur/GPU).
Les onglets masqués passent en `MemoryUsageTargetLevel::Low`, et les onglets restaurés ne sont
créés qu'au premier clic.

Données : `%APPDATA%\Vanta` (settings.json, bookmarks.json, session.json, history.sqlite,
block_stats.json, profil WebView2).

## Traductions

Le texte source est en **français**, directement dans le code. L'anglais vient d'un dictionnaire :

- `ui/i18n-en.json` : `exact` (texte français -> anglais) et `patterns`, des modèles avec
  trous numérotés (`["{1} favori(s)", "{1} bookmark(s)"]`) ;
- `ui/i18n.js` : chargé en premier par chaque page interne (`vanta://i18n.js`, précédé de la
  langue et du dictionnaire), il traduit les textes et les attributs `title`, `placeholder`…
  dès qu'ils apparaissent (MutationObserver). Un élément `data-notr` (titres de pages, notes,
  favoris) n'est jamais traduit ; `data-en-html` donne la version anglaise d'un titre mis en forme ;
- `src/i18n.rs` : `tr()` pour les textes affichés par Windows (boîtes de message, menu
  contextuel, titres de fenêtres) ;
- l'installateur a son propre dictionnaire (`installer/ui/setup-en.json`) et réutilise `ui/i18n.js`.

Pour ajouter un texte : l'écrire en français, puis ajouter sa traduction dans le dictionnaire.

## Sécurité

- Les pages internes `vanta://` ont accès à l'API de Vanta ; Rust vérifie l'**origine exacte**
  (`https://vanta.localhost/`) de chaque message, les pages web n'y ont pas accès.
- Mode lecture : l'article extrait d'un site est nettoyé (liste blanche de balises, liens et
  images http(s) seulement) puis affiché dans une iframe `sandbox` sans script, avec sa propre CSP.
- Raccourcis clavier capturés **nativement** (WebView2 `AcceleratorKeyPressed`) : une page ne
  peut pas les déclencher.
- Pages internes servies avec une CSP stricte, `frame-ancestors 'none'` et `nosniff` ;
  l'interface et le menu déroulant ne peuvent pas quitter leur page.
- Toutes les données affichées sont échappées ; seules les adresses `http(s)` sont acceptées
  pour les favoris, applis du panneau et liens externes (pas de `javascript:`).
- SmartScreen (Microsoft) actif par défaut, désactivable dans les réglages.
- Mises à jour signées (Ed25519 sur version + SHA-256) : un fichier modifié ou une ancienne
  version renommée est refusé, même si le dépôt GitHub était compromis.
- `cargo audit` : aucune vulnérabilité connue dans les dépendances.

## Limites connues (V1)

- La RAM d'un onglet reste celle de Chromium : le gain vient de la suspension/déchargement et du
  chargement paresseux, pas d'un moteur plus léger.
- Le plafond CPU s'applique à tout Vanta (interface comprise), pas onglet par onglet.
- Extensions : pas de bouton d'extension dans la barre ; le popup s'ouvre dans un onglet
  (bouton ↗ dans les réglages, chemin `popup.html` supposé).
- Pas encore de suggestions dans la barre d'adresse ni de menu clic droit natif sur les onglets
  (une barre d'actions le remplace, car les menus HTML seraient masqués par la page).

## Tests de sécurité

- `cargo test` : paquets CRX de test de Chromium (`tests/data/crx`, licence BSD) pour la
  vérification des extensions ; règles de `security.rs` (origine exacte des pages internes, liens externes
  bloqués, téléchargements trompeurs, accès aux ressources internes…).
- `tools/xss-test` : charge chaque page de `ui/` dans un navigateur simulé (jsdom) avec des
  titres, adresses, noms de fichiers et suggestions piégés, et vérifie qu'aucun code ne peut
  s'y exécuter ; `autoplay-test.js` vérifie la garde de lecture automatique. Nécessite Node.js :

  ```powershell
  cd tools\xss-test
  npm install
  npm test
  ```

## Tests du bloqueur

- `cargo test blocker` : règles de Vanta, scriptlets (liste ordinaire / de confiance, garde,
  cache), ressources `$redirect=`, exception LinkedIn ; avec les listes et ressources réelles si
  elles sont dans `/tmp/lists` et `/tmp/ubo-resources.json` (pubs vidéo YouTube : json-prune).
- `node tools\adguard-test\test.js` : garde anti-pubs (`src/adguard.js`) dans une page
  simulée : réponses fetch / XHR du lecteur YouTube, `ytInitialPlayerResponse`, pub passée,
  cadre replié, GPC, anti-empreinte (export bruité stable, original intact, audio). Sans dépendance.
- `docs/ubo/resources.json` se régénère depuis un clone de uBlock Origin (le code n'est jamais
  exécuté, seulement lu) :

  ```powershell
  git clone --depth 1 https://github.com/gorhill/uBlock $env:TEMP\ubo
  python tools\ubo-resources\build.py $env:TEMP\ubo docs\ubo\resources.json
  ```

  puis mettre à jour le commit dans `docs/ubo/LICENSE.txt` et lancer `publish-readme.ps1`.
