# CLAIA — Personal shopper IA pour la mode

> Prototype interactif d'un styliste personnel propulsé par l'IA : il compose des tenues complètes adaptées à ta silhouette, à l'occasion et à ton style, puis te laisse changer chaque pièce une par une.

Projet réalisé en mars–avril 2026, en autonomie, à partir d'un constat simple : les outils de recherche des sites de mode fonctionnent comme des moteurs de recherche froids. Ils renvoient des pièces isolées, sans narration ni coordination de tenue. CLAIA imagine ce que pourrait être un vrai personal shopper en ligne pour une marque de prêt-à-porter premium (l'exemple utilisé est un catalogue type Sandro Paris).

<!-- Démo en ligne : https://LIEN-A-AJOUTER -->

![Aperçu du prototype](images/1re-tenue-generee-prototype.png)

---

## Fonctionnalités

Le prototype est organisé en **4 onglets** :

### 1. Découvrir
L'utilisateur renseigne son profil (**morphologie, occasion, styles préférés, budget**) et CLAIA génère une **tenue principale + 4 alternatives**.
- Chaque tenue est présentée **sur un mannequin correspondant à la silhouette choisie**.
- **Carrousel pièce par pièce** : le haut, le bas et les chaussures sont remplaçables indépendamment, et le visuel du mannequin se met à jour avec la variante choisie.
- Chaque pièce affiche son nom, sa marque et son prix.

### 2. Style Icons & Cinéma
18 références culturelles (films, séries, personnages, époques) traduites en tenues achetables.
*Ex. : Gossip Girl → robe longue à sequins et escarpins argentés ; Clueless → blouson en jean sur une robe paisley.*

### 3. Recherche visuelle
L'utilisateur **glisse ou importe une photo** qui l'inspire (magazine, Instagram, street style), affine avec des filtres (type de pièce, catégorie, « même style / plus habillé / plus casual », budget) et obtient des **alternatives équivalentes dans le catalogue**.

### 4. Ma Sélection
Recherche en langage naturel : l'utilisateur tape par exemple *« une tenue pour un dîner élégant mais pas trop »* et l'IA recommande les tenues les plus adaptées, avec une explication.

---

## Comment c'est construit

| Brique | Rôle |
|---|---|
| **HTML / CSS / JavaScript** (vanilla, un seul fichier) | Interface et logique de recommandation (scoring des tenues par occasion, style et ambiance) |
| **Kling AI** | Génération des visuels de *virtual try-on* : les tenues portées par des mannequins de différentes morphologies |
| **API Claude (Anthropic)** | Compréhension des requêtes en langage naturel dans « Ma Sélection » |
| **Netlify Functions** | Petit proxy côté serveur qui appelle l'API Claude, pour ne pas exposer la clé d'API dans le navigateur et contourner les restrictions CORS |
| **GitHub** | Hébergement du code et des images |

Chaque tenue est décrite comme un objet de données (pièces, prix, variantes, visuels par morphologie, tags d'occasion, de style et d'ambiance), ce qui permet d'en ajouter de nouvelles sans toucher à l'interface.

---

## Structure du projet

```
claia/
├── index.html                 # Le prototype (interface + logique)
├── images/                    # Photos des pièces, tenues générées, mannequins
└── netlify/
    └── functions/
        └── claude.js          # Proxy vers l'API Claude
```

---

## Lancer le projet en local

**Version simple (sans la recherche IA)** : clone le dépôt et ouvre `index.html` dans ton navigateur.

```bash
git clone https://github.com/bnmarty2-create/claia.git
cd claia
open index.html   # ou double-clic sur le fichier
```

**Avec la recherche IA (« Ma Sélection »)** : il faut une clé d'API Anthropic et la [CLI Netlify](https://docs.netlify.com/cli/get-started/).

```bash
npm install -g netlify-cli
export ANTHROPIC_API_KEY="ta-cle-ici"   # ne jamais la mettre dans le code
netlify dev
```

---

## Limites actuelles

- **Catalogue réduit** : une dizaine de tenues complètes, ce qui limite la finesse des recommandations.
- **Try-on pré-généré** : les visuels mannequin ont été générés en amont avec Kling AI, ils ne sont pas calculés en temps réel.
- **Recherche visuelle simulée** : l'interface est en place, mais l'analyse d'image n'est pas encore branchée sur un vrai modèle de vision.

## Pistes d'évolution

- Étendre le catalogue (30+ pièces étiquetées automatiquement) pour multiplier les combinaisons.
- Brancher un modèle de *virtual try-on* en temps réel.
- Connecter la recherche visuelle à un modèle multimodal.
- Ajouter une « garde-robe » personnelle pour proposer des tenues avec les vêtements que l'utilisateur possède déjà.

---

## Auteur

**Benjamin Marty**, étudiant à HEC Paris (Master in Management)

---

*Prototype étudiant à visée de démonstration, sans lien avec les marques citées. Les photos de produits appartiennent à leurs propriétaires respectifs.*
