# Versions de Vanta : GitHub et Microsoft Store

Vanta est publié de deux façons :

| | Signature | Où | Mises à jour |
|---|---|---|---|
| **GitHub** (`VantaSetup.exe`) | non signé : Windows affiche un avertissement, et le *contrôle intelligent des applications* peut le bloquer | GitHub Releases | par Vanta |
| **Microsoft Store** | paquet signé par Microsoft : jamais bloqué | Microsoft Store | par le Store |

Les deux sont gratuits. Le Store affiche le nom d'éditeur que tu choisis (ton pseudo), pas ton nom.

> Signer l'installateur GitHub demanderait un certificat de signature de code payant (le service
> de Microsoft, *Azure Artifact Signing*, n'est de plus pas ouvert aux particuliers en France).
> C'est pourquoi la version signée passe par le Store, gratuit.

---

## Publier sur le Microsoft Store

Le Store est gratuit pour les développeurs particuliers. Microsoft signe le paquet : une
appli installée depuis le Store n'est jamais bloquée par SmartScreen ni par le contrôle
intelligent des applications.

### 1. Une seule fois : compte et identité

1. Crée un compte développeur **individuel** (gratuit) sur https://storedeveloper.microsoft.com
   avec ton compte Microsoft. Microsoft vérifie ton identité (non publique) ; le **nom
   d'éditeur affiché** est celui que tu choisis, par exemple ton pseudo.
2. Dans le **Partner Center** : *Applications et jeux › Nouveau produit › Application MSIX ou
   PWA*, puis réserve le nom (« Vanta » s'il est libre, sinon une variante comme « Vanta
   Browser » : mets-la aussi dans `display_name`).
3. *Gestion des produits › Identité du produit* : recopie les trois valeurs dans
   `packaging\msix\store.json` :
   - `Package/Identity/Name` → `identity_name`
   - `Package/Identity/Publisher` → `publisher` (de la forme `CN=…`)
   - `Package/Properties/PublisherDisplayName` → `publisher_display_name`
4. Installe le SDK Windows : `winget install Microsoft.WindowsSDK.10.0.26100`

### 2. Créer et envoyer le paquet

```powershell
.\build-msix.ps1
```

Il crée `dist\Vanta-<version>.msix` à partir de `dist\vanta.exe` (la dernière version
compilée par `publish-release.ps1`). Raccourci : `.\publish-release.ps1 -Version x.y.z -Notes "…" -Store`
publie sur GitHub et crée le paquet du Store en une fois. Dans la soumission du Partner Center :

- **Packages** : envoie le fichier `.msix` ;
- **Tarification** : gratuit ;
- **Propriétés** : catégorie *Utilitaires et outils* (ou *Productivité*), et l'adresse de la
  politique de confidentialité :
  `https://github.com/iZeyros/Vanta-browser/blob/main/docs/CONFIDENTIALITE.md` ;
- **Classification par âge** : réponds au questionnaire (navigateur web : accès illimité à Internet) ;
- **Fonctionnalité restreinte `runFullTrust`** : justification à coller :
  *« Vanta est un navigateur de bureau Win32. Il a besoin d'un accès complet pour gérer ses
  fenêtres, enregistrer les téléchargements dans le dossier de l'utilisateur et limiter
  ses propres ressources (Job Object Windows). »*
- **Fiche du Store** : description, captures d'écran (`docs/screenshots`).

La certification prend en général un à trois jours. Pour chaque nouvelle version : crée le
paquet (`-Store` ou `.\build-msix.ps1`) puis une nouvelle soumission avec ce paquet.

Dans la version du Store, Vanta ne se met pas à jour lui-même (le Store s'en charge) et
l'option « Lancer au démarrage de Windows » est masquée.

### Essayer le paquet sur ton PC

```powershell
.\build-msix.ps1 -Test
```

Le script signe le paquet avec un certificat de test et affiche la commande (à lancer une
fois en administrateur) pour faire confiance à ce certificat, avant le double-clic sur le `.msix`.

---

## À savoir

- Les deux versions peuvent être installées en même temps : ce sont deux applications distinctes
  pour Windows.
- Sur ton propre PC, les compilations locales (`cargo run`) ne sont pas signées. Si le
  contrôle intelligent des applications les bloque, tu peux le désactiver puis le
  réactiver plus tard : *Sécurité Windows › Contrôle d'applications et du navigateur ›
  Paramètres du contrôle intelligent des applications*.
