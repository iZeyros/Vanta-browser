## Vanta 0.3.0

### Plusieurs fenêtres
- **Onglet détaché** : glisse un onglet hors de la barre d'onglets (sur la page ou hors de la fenêtre) et il part dans sa propre fenêtre, sans recharger la page. Lâché sur une autre fenêtre Vanta, il la rejoint. Aussi : clic droit sur un onglet › *Nouvelle fenêtre*.
- **Nouvelle fenêtre** : Ctrl+N, ou relancer Vanta alors qu'il est déjà ouvert (avant, la 2e fenêtre se fermait aussitôt).
- Toutes les fenêtres partagent les réglages, les favoris, le VPN et le bloqueur, et sont restaurées au redémarrage. Fermer le dernier onglet d'une fenêtre ferme la fenêtre (s'il en reste d'autres).

### Fenêtre Tor
- Nouveau bouton **oignon** dans le panneau latéral (entre le bloc-notes et la navigation privée), ou **Ctrl+Maj+X** : une fenêtre privée où **tout passe par le réseau Tor**, sans pouvoir le couper.
- **Sites en .onion** accessibles ; un lien .onion ouvert dans une fenêtre normale s'ouvre automatiquement dans la fenêtre Tor. Clic droit sur un lien › *Ouvrir le lien dans la fenêtre Tor*.
- Le plus anonyme possible : fuseau horaire UTC et langue anglaise présentés aux sites, WebRTC bloqué, empreinte brouillée, SmartScreen et suggestions coupés, recherche par DuckDuckGo en .onion, réseau local injoignable depuis les pages, rien de conservé à la fermeture. Badge **TOR** et *Nouvelle identité* dans la barre d'adresse.

### Thèmes complets, sons et musique
- **Thèmes en un clic**, comme les mods d'Opera GX : *Lofi*, *Synthwave*, *Espace*, *Sakura*, *Arcade*, *Atelier*, *Mécanique* (et *Vanta* pour revenir à l'origine). Chacun change les couleurs, la police, la forme des onglets, le fond d'écran animé, les sons et la musique.
- **Crée tes thèmes** : retouche ce que tu veux puis *Enregistrer ma configuration comme thème*. **Exporte**-le en fichier `.vantatheme` (avec ton fond d'écran et tes sons) pour le partager, et **importe** ceux des autres.
- **Sons de frappe** partout : barre d'adresse, pages de Vanta et champs des sites (les sites ne savent jamais quelle touche tu tapes). Packs générés : Mécanique, Doux, Rétro 8-bit, Machine à écrire, Bulles. **Tes propres sons** (WAV, MP3, OGG) pour chaque touche, clic, onglet et notification. Volume réglable.
- **Musique de fond** composée en direct par Vanta (Lofi, Synthwave, Ambiance, Chiptune) : aucune musique sous droits, aucun fichier ni connexion. Elle ne joue que quand Vanta est au premier plan, se coupe en mode jeu et quand un onglet joue du son.
- **Nouveaux fonds d'écran animés** : pluie (lofi), étoiles filantes, pétales.
- **Style** : police de l'interface (technique, code, élégante, manuscrite), forme des onglets (biseautés, arrondis, droits), effet néon, animations réduites.

### Paramètres
- **Barre de recherche** : tape « musique », « pub », « ram »… et seuls les réglages correspondants restent (raccourci « / » ou Ctrl+F).
- **Réorganisés** en groupes : Général, Apparence (thèmes, couleurs & style, fond d'écran, sons & musique, mise en page), Performances, Confidentialité, Jeux, Navigation, Système.

### Personnalisation
- **Thème sur mesure** : choisis le thème *Personnalisé* puis ta couleur de fond, de texte et l'arrondi des coins ; les surfaces, lignes et textes secondaires en sont dérivés (thème clair ou sombre selon le fond).
- **Barre d'outils à la carte** : affiche ou masque chaque bouton (précédent, accueil, mesure RAM / CPU, lecteur réduit, capture, écran partagé, extensions, téléchargements, notifications) et change leur ordre ; idem pour les boutons de la barre d'adresse (traduire, lecture, bouclier, VPN, favori).
- **Page d'accueil personnalisable** : choisis les blocs affichés (logo, nouvelle **horloge**, recherche, statistiques, sites fréquents, liste de souhaits, jeux gratuits) et leur ordre.
- **Mise en page** : mode compact (barres plus basses), largeur des onglets (étroits, normaux, larges), barre latérale à gauche, à droite ou masquée.
- Tout est dans *Paramètres › Apparence*, avec un bouton pour revenir à la présentation d'origine.

### Capture d'écran
- **Ctrl+Maj+S**, le bouton de la barre d'outils ou clic droit › *Capture d'écran* : sélectionne une zone à la souris, ou capture la partie visible ou la **page entière**.
- L'image est enregistrée en PNG dans *Images › Vanta* et copiée dans le presse-papiers (à coller dans Discord, un document…) ; la notification propose *Ouvrir* et *Dossier*.

### Mode sombre forcé
- *Paramètres › Apparence › Couleurs & style › Mode sombre forcé sur les sites* : les sites sans thème sombre sont assombris automatiquement par le moteur.
- Exceptions par site dans le menu du cadenas (*Oui* / *Non* / *Défaut*), par exemple pour l'activer seulement sur un site trop clair.

### Démarrage
- Plus d'écran blanc à l'ouverture de Vanta et de l'installateur : la fenêtre prend tout de suite la couleur du thème, avec le logo de Vanta pendant le chargement.

### Clic droit
- **Liens** : « Ouvrir le lien dans un nouvel onglet » (en arrière-plan) remplace « Ouvrir le lien dans une nouvelle fenêtre », qui ouvrait en fait un onglet ; « Ouvrir le lien dans une fenêtre privée » est toujours là.
- **Images** : « Ouvrir l'image dans un nouvel onglet ».
- **Texte sélectionné** : « Rechercher « … » sur le web » avec ton moteur de recherche.
- **Page d'un site** : « Traduire la page » et « Mode lecture ».
- **Barre d'adresse et bloc-notes** : le clic droit ouvre enfin le menu d'édition (couper, copier, coller, tout sélectionner, orthographe). Dans la barre d'adresse : « Coller et y aller ».
- **Pages de Vanta** : toujours sans les outils inutiles (inspecter, imprimer, enregistrer…).

### Raccourcis clavier
- **Nouveaux** : Ctrl+N (nouvelle fenêtre), Ctrl+M (couper le son de l'onglet), Ctrl+Maj+PgSuiv / PgPréc (déplacer l'onglet), Ctrl+Maj+B (barre de favoris), Alt+P (paramètres), Ctrl+Maj+Suppr (effacer les données), Alt+Début (page d'accueil), Ctrl+Maj+J (console).
- **Clic du milieu ou Ctrl+clic sur un lien** : l'onglet s'ouvre en arrière-plan, comme dans Chrome (Ctrl+Maj+clic : au premier plan).
- **Ctrl+U** (source de la page) fonctionne.
- **Ctrl+Espace ne recherche plus les onglets** (il gênait la complétion des éditeurs de code en ligne, les tableurs et le changement de langue de saisie de Windows) : c'est **Ctrl+Maj+A**.
- **Mêmes raccourcis partout** : quand la barre d'adresse a le focus, Ctrl+1…9, Ctrl+Maj+O, F12, Ctrl+F4… fonctionnent aussi.
- **Barre d'adresse** : AltGr (@, #, €…) ne déclenche plus de raccourci par erreur ; Ctrl+0 remet le zoom à 100 % aussi sur un clavier AZERTY.
- Liste complète : *Paramètres › Raccourcis clavier*.

---

### Texte « Nouveautés de cette version » pour le Microsoft Store (copier-coller)

Fenêtre Tor (Ctrl+Maj+X) pour naviguer anonymement et accéder aux sites .onion. Thèmes complets façon mods (Lofi, Synthwave, Espace, Sakura…) avec fond d'écran animé, sons de frappe et musique de fond générée ; crée, exporte et importe tes thèmes, tes propres sons. Recherche dans les paramètres. Personnalisation : thème sur mesure (fond, texte, arrondi), barre d'outils et page d'accueil à la carte (avec une horloge), mode compact, barre latérale à droite ou masquée. Capture d'écran (Ctrl+Maj+S) d'une zone, de la partie visible ou de la page entière, enregistrée et copiée. Mode sombre forcé sur les sites, avec exceptions par site. Plusieurs fenêtres : glisse un onglet hors de la fenêtre pour le détacher (sans recharger la page), Ctrl+N pour une nouvelle fenêtre, et Vanta peut être relancé alors qu'il est déjà ouvert. Plus d'écran blanc au démarrage. Clic droit amélioré : ouvrir un lien ou une image dans un nouvel onglet, rechercher le texte sélectionné, traduire la page, mode lecture, et menu copier-coller dans la barre d'adresse (avec « Coller et y aller »). Nouveaux raccourcis (Ctrl+M pour couper le son d'un onglet, Ctrl+Maj+B pour la barre de favoris, Alt+P pour les paramètres…), clic du milieu sur un lien = onglet en arrière-plan, et liste de tous les raccourcis dans les paramètres. La recherche d'onglets passe à Ctrl+Maj+A.

### “What's new in this version” for the English Store listing (copy and paste)

Tor window (Ctrl+Shift+X) to browse anonymously and reach .onion sites. Full themes like mods (Lofi, Synthwave, Space, Sakura…) with animated wallpaper, typing sounds and generated background music; create, export and import themes, use your own sounds. Search in settings. Customization: custom theme (background, text, corner rounding), choose and reorder the toolbar buttons and the home page blocks (now with a clock), compact mode, sidebar on the right or hidden. Screenshots (Ctrl+Shift+S) of an area, the visible part or the full page, saved and copied. Forced dark mode on websites, with per-site exceptions. Multiple windows: drag a tab out of the window to detach it (the page doesn't reload), Ctrl+N opens a new window, and Vanta can be launched again while it's already open. No more white screen at startup. Better right-click menus: open a link or an image in a new tab, search the selected text, translate the page, reader mode, and a copy-paste menu in the address bar (with “Paste and go”). New shortcuts (Ctrl+M to mute a tab, Ctrl+Shift+B for the bookmarks bar, Alt+P for settings…), middle-click on a link opens a background tab, and every shortcut is listed in the settings. Tab search moves to Ctrl+Shift+A.
