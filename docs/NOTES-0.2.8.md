## Vanta 0.2.8

### Nouveautés
- **Liste de souhaits et alertes de prix** : ajoute des jeux depuis l'accueil (champ « Ajouter un jeu à suivre »). Vanta affiche le meilleur prix toutes boutiques (Steam, Epic, GOG, Humble, Fanatical…, service CheapShark, prix en dollars US) et le plus bas historique, et t'envoie une notification quand un jeu de ta liste passe en promo. La réduction minimale se règle dans *Paramètres › Liste de souhaits* (-20 %, -50 %, -75 % ou -90 %) ; le plus bas historique est toujours signalé.
- **Protection contre les empreintes** : les sites qui identifient ton navigateur par le dessin d'une image (canvas, WebGL) ou un son calculé reçoivent un résultat légèrement brouillé, différent sur chaque site et à chaque lancement. Rien de visible ni d'audible ; désactivée avec le bloqueur sur les sites autorisés (*Paramètres › Bloqueur & confidentialité*).

### Bloqueur de pubs
- **Pubs vidéo YouTube** (avant, pendant et après les vidéos) : prise en charge des scriptlets de uBlock Origin et de sa liste de correctifs rapides (« quick fixes »), mise à jour en continu pour YouTube. Les réponses du lecteur (`playerAds`, `adPlacements`, `adSlots`) sont nettoyées avant d'arriver au lecteur, y compris au premier affichage d'une vidéo ; une pub qui passerait quand même est passée aussitôt.
- **Ressources de remplacement** (`$redirect=`) : un script neutre ou un pixel transparent est servi à la place d'un traqueur quand la liste le demande, pour que les sites qui en dépendent continuent de fonctionner.
- **Cadres publicitaires bloqués** repliés au lieu de laisser un encart vide.
- **Encarts LinkedIn** (bouton « Suivre », publications intégrées) : ne sont plus bloqués par erreur.
- **Sites autorisés** : le masquage des emplacements de pubs ne s'applique plus sur un site pour lequel le bloqueur est désactivé.
- **Confidentialité** : signal Global Privacy Control envoyé aux sites ; API publicitaires de Chromium désactivées (Protected Audience, Attribution Reporting, Shared Storage, Private Aggregation).

### Correctifs
- **Raccourci du VPN** : **Ctrl+Maj+E** remplace Alt+Maj+N, que Windows utilise pour changer la langue du clavier (le VPN ne s'activait pas).
- **Accueil** : la RAM affichée n'est plus « 0 Mo » juste après le démarrage, et elle se met à jour toute seule.
- Les noms de langue ne sont plus traduits dans les listes déroulantes.

---

### Texte « Nouveautés de cette version » pour le Microsoft Store (copier-coller)

(Si la 0.2.7 n'a pas été publiée sur le Store, coller d'abord le texte de `docs/NOTES-0.2.7.md` en remplaçant « Alt+Maj+N » par « Ctrl+Maj+E ».)

Liste de souhaits de jeux sur l'accueil avec alertes de prix : meilleur prix toutes boutiques (Steam, Epic, GOG, Humble…) et notification dès qu'un jeu passe en promo. Bloqueur renforcé sur YouTube : les pubs vidéo avant, pendant et après les vidéos sont bloquées grâce aux scriptlets de uBlock Origin. Nouvelle protection contre les empreintes (canvas, audio), signal Global Privacy Control et API publicitaires de Chromium désactivées. Cadres publicitaires repliés, encarts LinkedIn rétablis. Raccourci du VPN : Ctrl+Maj+E.

### “What's new in this version” for the English Store listing (copy and paste)

(If 0.2.7 was not published on the Store, first paste the text from `docs/NOTES-0.2.7.md`, replacing “Alt+Shift+N” with “Ctrl+Shift+E”.)

Game wishlist on the start page with price alerts: best price across stores (Steam, Epic, GOG, Humble…) and a notification as soon as a game goes on sale. Stronger blocker on YouTube: video ads before, during and after videos are blocked thanks to uBlock Origin scriptlets. New fingerprinting protection (canvas, audio), Global Privacy Control signal and Chromium's advertising APIs disabled. Blocked ad frames collapsed, LinkedIn embeds work again. VPN shortcut: Ctrl+Shift+E.
