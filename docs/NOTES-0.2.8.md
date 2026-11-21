## Vanta 0.2.8

### Bloqueur de pubs
- **Pubs vidéo YouTube** (avant, pendant et après les vidéos) : prise en charge des scriptlets de uBlock Origin et de sa liste de correctifs rapides (« quick fixes »), mise à jour en continu pour YouTube. Les réponses du lecteur (`playerAds`, `adPlacements`, `adSlots`) sont nettoyées avant d'arriver au lecteur, y compris au premier affichage d'une vidéo ; une pub qui passerait quand même est passée aussitôt.
- **Ressources de remplacement** (`$redirect=`) : un script neutre ou un pixel transparent est servi à la place d'un traqueur quand la liste le demande, pour que les sites qui en dépendent continuent de fonctionner.
- **Cadres publicitaires bloqués** repliés au lieu de laisser un encart vide.
- **Encarts LinkedIn** (bouton « Suivre », publications intégrées) : ne sont plus bloqués par erreur.
- **Sites autorisés** : le masquage des emplacements de pubs ne s'applique plus sur un site pour lequel le bloqueur est désactivé.
- **Confidentialité** : signal Global Privacy Control envoyé aux sites ; API publicitaires de Chromium désactivées (Protected Audience, Attribution Reporting, Shared Storage, Private Aggregation).

### Correctifs
- Les noms de langue ne sont plus traduits dans les listes déroulantes.

---

### Texte « Nouveautés de cette version » pour le Microsoft Store (copier-coller)

Bloqueur de pubs renforcé sur YouTube : les pubs vidéo avant, pendant et après les vidéos sont bloquées grâce aux scriptlets de uBlock Origin. Cadres publicitaires repliés, encarts LinkedIn rétablis, signal Global Privacy Control envoyé aux sites et API publicitaires de Chromium désactivées.

### “What's new in this version” for the English Store listing (copy and paste)

Stronger ad blocker on YouTube: video ads before, during and after videos are blocked thanks to uBlock Origin scriptlets. Blocked ad frames are collapsed, LinkedIn embeds work again, the Global Privacy Control signal is sent to sites and Chromium's advertising APIs are disabled.
