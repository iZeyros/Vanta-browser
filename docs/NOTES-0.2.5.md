## Vanta 0.2.5

### Nouveautés
- **Interface en anglais** (choisie d'après la langue de Windows, modifiable dans les réglages), installateur compris.
- **Assistant de premier lancement** : langue, thème, recherche, bloqueur, jeux gratuits et import des favoris.
- **Barre d'adresse intelligente** : suggestions tirées de tes onglets, favoris et historique, complétion du site (« yout » → youtube.com), croix pour retirer une suggestion, et suggestions du moteur de recherche en option.
- **Mots-clés de recherche** : `yt minecraft`, `w Paris`, `steam`, `tw`, `gh`… et tes propres mots-clés.
- **Extensions du Chrome Web Store et des modules Edge** : bouton « + Ajouter à Vanta » sur la page d'une extension. Vanta vérifie la signature du paquet, te montre ses autorisations et la met à jour toute seule.
- **Bouton Extensions** dans la barre d'outils.
- **Alerte jeux gratuits** (au choix) : une notification quand un jeu devient gratuit sur Epic, Steam, GOG, Prime Gaming…
- **Bloc-notes** dans le panneau latéral.
- **Thèmes complets** : Vanta, Minuit, Néon, Forêt, Braise, Noir OLED.
- **Mode immersif** (F11) : plein écran sans barres.
- **Onglets épinglés**, **zoom retenu par site**, **demandes d'autorisation** (micro, caméra, position…) avec mémorisation par site.
- **Lecture automatique des vidéos bloquée** tant que tu n'as pas cliqué dans la page (réglable par site).
- **Récupération après un plantage** : page rechargée, onglets restaurés.
- **Export des favoris** en fichier HTML standard et **journal de diagnostic** local.
- Le panneau de ressources s'appelle désormais **Vanta Core**.

### Améliorations
- **Bloqueur bien plus efficace** : les requêtes bloquées échouent vraiment (avant, une réponse « interdit » laissait croire aux sites et aux tests que la connexion avait réussi), blocage dans les iframes et les service workers, masquage des emplacements de pubs sur tous les sites, listes uBlock Origin (vie privée, logiciels malveillants, corrections) et protection renforcée de 230 000 domaines (HaGeZi Pro). Nouveau niveau **Maximal** (bandeaux de cookies, connexion Facebook sur les autres sites, boutons de partage, discussions d'assistance, notifications des sites). Tests : adblock.turtlecute.org 130/130, superadblocktest.com 478/482 en Maximal.
- **Moins de RAM** : un processus par site, pas de pages préchargées en cachette, bloqueur plus léger, mémoire libérée en jeu et quand Vanta est réduit, onglets d'arrière-plan déchargés si Windows manque de RAM.
- **Démarrage plus rapide** : bloqueur prêt en quelques millisecondes.
- Réglages appliqués **immédiatement** partout (thème, accent, fond d'écran…), sans recharger les pages.
- Infobulles au style de Vanta ; plus de menu « Inspecter » sur les pages de Vanta.

### Sécurité
- Un site ne peut plus ouvrir les pages internes de Vanta ni lire ses ressources.
- Liens dangereux vers des outils de Windows bloqués (`ms-msdt:`, `search-ms:`…).
- Téléchargements : faux documents (« facture.pdf.exe ») bloqués, programmes reçus sans chiffrement mis en pause, confirmation avant d'ouvrir un programme.
- Mise à jour en administrateur vérifiée par la version installée.

---

### Texte « Nouveautés de cette version » pour le Microsoft Store (copier-coller)

Bloqueur de pubs et traqueurs bien plus efficace (vrais échecs réseau, iframes, masquage sur tous les sites, 230 000 domaines en protection renforcée). Interface en français ou en anglais et assistant de premier lancement. Barre d'adresse avec suggestions et mots-clés de recherche (yt, w, steam…). Extensions du Chrome Web Store et des modules Edge en un clic. Alerte jeux gratuits (au choix), bloc-notes dans le panneau latéral, thèmes complets (Minuit, Néon, Forêt, Braise, Noir OLED) et mode immersif (F11). Onglets épinglés, zoom retenu par site, demandes d'autorisation par site, lecture automatique des vidéos bloquée. Moins de RAM, démarrage plus rapide, récupération après un plantage et nombreux correctifs de sécurité. Le panneau de ressources s'appelle désormais Vanta Core.

### “What's new in this version” for the English Store listing (copy and paste)

Much stronger ad and tracker blocker (real network failures, iframes, ad slots hidden on every site, 230,000 domains in strong mode). English interface and first-run setup assistant. Address bar suggestions and search keywords (yt, w, steam…). One-click extensions from the Chrome Web Store and Microsoft Edge Add-ons. Optional free games alert, notepad in the side panel, full themes (Midnight, Neon, Forest, Ember, OLED black) and immersive mode (F11). Pinned tabs, per-site zoom, per-site permission prompts, autoplay blocked. Less RAM, faster startup, crash recovery and many security fixes. The resources panel is now called Vanta Core.
