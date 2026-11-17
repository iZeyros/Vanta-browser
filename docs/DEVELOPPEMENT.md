# Vanta — documentation développeur

> Présentation et téléchargement : voir le [README](../README.md).

Navigateur Windows inspiré d'Opera GX, écrit en Rust avec **WebView2** (le moteur Chromium
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
| **GX Control** | Limiteur **RAM** (suspension puis déchargement des onglets les plus anciens), plafond **CPU** strict (Job Object Windows), limiteur **réseau** par onglet (DevTools Protocol), suspension auto des onglets inactifs, graphiques en direct |
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
  storage.rs     paramètres, favoris, session, téléchargements (JSON) + historique (SQLite)
  blocker.rs     listes de filtres + moteur adblock-rust
  import.rs      import Chromium (Bookmarks JSON, History SQLite)
  games.rs       flux des jeux gratuits (GamerPower, cache 1 h)
  sysmon.rs      RAM/CPU de Vanta + tous ses processus WebView2
  win/mod.rs     fenêtre tao, WebView enfants, IPC, politique mémoire, limiteurs
  win/native.rs  COM WebView2 (requêtes, CDP, suspension, audio, extensions),
                 Job Object CPU, détection de jeu plein écran
  win/pages.rs   pages internes vanta:// embarquées + script injecté dans les onglets
  favicons.rs    cache des icônes de sites
ui/              interface (chrome.html) et pages internes (start, settings, history…)
assets/          icône de l'application (vanta.ico, app-icon.svg)
installer/       VantaSetup : installateur / désinstalleur (Rust + WebView2)
crates/vanta-update/  mises à jour : GitHub Releases, téléchargement, signature Ed25519
tools/release/   vanta-release : clé de signature + signature des versions
release.json     dépôt GitHub des mises à jour
```

Toutes les WebView partagent **un seul environnement WebView2** (mêmes processus navigateur/GPU).
Les onglets masqués passent en `MemoryUsageTargetLevel::Low`, et les onglets restaurés ne sont
créés qu'au premier clic.

Données : `%APPDATA%\Vanta` (settings.json, bookmarks.json, session.json, history.sqlite, profil WebView2).

## Sécurité

- Les pages internes `vanta://` ont accès à l'API de Vanta ; Rust vérifie l'**origine exacte**
  (`https://vanta.localhost/`) de chaque message, les pages web n'y ont pas accès.
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
