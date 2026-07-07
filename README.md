# 🏢 CONGLOMERAT

> **On peut !** — Annuaire moderne des entreprises camerounaises par ville, avec carte interactive, recherche intelligente et interface Liquid Glass.

**Auteur :** Crazy Prince Dev — Fullstack 2026  
**Pays cible :** Cameroun 🇨🇲  
**Villes de départ :** Douala · Yaoundé  
**Type de projet :** site statique 100% frontend, prêt pour Vercel

---

## ✨ Présentation

**CONGLOMERAT** est un annuaire web qui regroupe des entreprises camerounaises par ville. Le site permet de :

- explorer les entreprises sur une **carte interactive** ;
- rechercher une entreprise par nom, secteur, adresse ou hashtag ;
- filtrer par ville, catégorie, secteur et proximité ;
- consulter les informations utiles : téléphone, site web, adresse, Google Maps ;
- proposer une nouvelle entreprise via un formulaire EmailJS ;
- ajouter de nouvelles villes ou entreprises simplement avec des fichiers JSON.

Le projet ne dépend d’aucune base de données ni d’aucun backend : tout est géré côté frontend.

---

## 🧰 Stack utilisée

| Domaine | Outils / techniques |
|---|---|
| Structure | HTML5 sémantique |
| Style | CSS3, variables CSS, Grid, Flexbox |
| Interface | Liquid Glass, responsive mobile-first |
| Logique | JavaScript vanilla ES6+ |
| Carte | Leaflet.js |
| Clustering | Leaflet.markercluster |
| Recherche | Fuse.js |
| Formulaire | EmailJS |
| Icônes | Font Awesome 6 |
| Images | URLs Cloudinary / Unsplash dans les JSON |
| Données | JSON statiques |
| Déploiement | Vercel |
| Internationalisation | FR / EN via fichiers JSON |
| Thème | Dark / Light avec `localStorage` |

---

## 📁 Structure du projet

```txt
/
├── index.html
├── entreprises.html
├── documentation.html
├── mentions-legales.html
├── confidentialite.html
├── README.md
├── vercel.json
└── assets/
    ├── css/
    │   ├── main.css
    │   ├── glass.css
    │   ├── animations.css
    │   └── responsive.css
    ├── js/
    │   ├── app.js
    │   ├── loader.js
    │   ├── geolocation.js
    │   ├── map.js
    │   ├── data-loader.js
    │   ├── search-filter.js
    │   ├── modal-cta.js
    │   ├── contact-form.js
    │   └── i18n.js
    ├── data/
    │   ├── villes.json
    │   ├── entreprises-douala.json
    │   └── entreprises-yaounde.json
    ├── img/
    │   ├── social-preview.png
    │   └── logo/
    │       ├── logo-full.svg
    │       ├── logo-icon.svg
    │       ├── favicon.png
    │       ├── favicon.ico
    │       ├── apple-touch-icon.png
    │       └── safari-pinned-tab.svg
    └── locales/
        ├── fr.json
        └── en.json
```

---

## 🗺️ Fonctionnalités principales

### Carte interactive

La page `entreprises.html` utilise **Leaflet.js** avec les tuiles CartoDB :

- thème sombre : `dark_all` ;
- thème clair : `light_all` ;
- regroupement des points avec `Leaflet.markercluster` ;
- marqueur spécial pour la position utilisateur ;
- clic sur une fiche entreprise pour centrer la carte sur le marqueur.

### Recherche et filtres

La recherche est gérée avec **Fuse.js** pour permettre une recherche floue sur :

- nom de l’entreprise ;
- secteur ;
- catégorie ;
- hashtags ;
- adresse.

Les filtres disponibles sont :

- ville ;
- catégorie ;
- secteur ;
- proximité, si la géolocalisation est disponible.

### Internationalisation FR / EN

Le site charge les traductions depuis :

```txt
assets/locales/fr.json
assets/locales/en.json
```

La langue sélectionnée est sauvegardée dans `localStorage`.

Les descriptions d’entreprises utilisent directement les champs :

```json
"description": "Texte en français",
"description_en": "English text"
```

### Thème sombre / clair

Le thème sombre est activé par défaut. Le changement de thème :

- modifie l’attribut `data-theme` sur `<html>` ;
- met à jour les variables CSS ;
- change les tuiles Leaflet sans recharger la page ;
- sauvegarde la préférence dans `localStorage` ;
- met à jour la couleur navigateur via `theme-color`, utile notamment pour Safari mobile.

### Preview réseaux sociaux

Le site contient les métadonnées Open Graph et Twitter Card :

- titre ;
- description ;
- image de preview ;
- dimensions d’image ;
- alt text.

Image utilisée :

```txt
assets/img/social-preview.png
```

---

## 🧾 Gestion des données

Les villes sont déclarées dans :

```txt
assets/data/villes.json
```

Chaque ville référence son propre fichier d’entreprises :

```json
{
  "id": "douala",
  "nom": "Douala",
  "center": [4.0511, 9.7679],
  "fichier": "assets/data/entreprises-douala.json"
}
```

### Ajouter une entreprise

Ouvrir le fichier de la ville concernée, par exemple :

```txt
assets/data/entreprises-douala.json
```

Puis ajouter une entrée dans le tableau `entreprises` :

```json
{
  "id": "dla-017",
  "nom": "Nom de l’entreprise",
  "secteur": "Secteur d’activité",
  "categorie": "SA",
  "hashtags": ["#industrie", "#services"],
  "description": "Description en français.",
  "description_en": "English description.",
  "image": "https://example.com/image.jpg",
  "latitude": 4.0511,
  "longitude": 9.7679,
  "adresse": "Adresse complète",
  "telephone": "+237 6XX XXX XXX",
  "siteweb": "https://example.com",
  "verifie": true
}
```

Catégories acceptées :

```txt
SARL · SA · Ets · Commerce · Boutique · Marché · Usine · Coopérative
```

### Ajouter une nouvelle ville

1. Créer un fichier :

```txt
assets/data/entreprises-bafoussam.json
```

2. Ajouter la ville dans `villes.json` :

```json
{
  "id": "bafoussam",
  "nom": "Bafoussam",
  "nom_en": "Bafoussam",
  "region": "Ouest",
  "icone": "fa-city",
  "center": [5.4781, 10.4176],
  "zoom": 12,
  "fichier": "assets/data/entreprises-bafoussam.json",
  "description": "Pôle économique majeur de la région de l’Ouest.",
  "description_en": "Major economic hub in the West region."
}
```

Aucune modification JavaScript n’est nécessaire.

---

## 📬 Formulaire EmailJS

Le formulaire “Proposer mon entreprise” utilise EmailJS.

Fichier concerné :

```txt
assets/js/contact-form.js
```

Configuration actuelle :

```js
emailjs.init("6l8UctmqC8QtD42mg");
const EMAILJS_TEMPLATE_ID = "A_COMPLETER";
```

À faire avant production :

```js
const EMAILJS_TEMPLATE_ID = "VOTRE_TEMPLATE_ID";
```

Le template EmailJS doit contenir ces variables :

```txt
{{name}}
{{time}}
{{message}}
```

Le message envoyé regroupe :

- nom de l’entreprise ;
- secteur ;
- ville ;
- téléphone ;
- description.

---

## 🚀 Déploiement sur Vercel

Le site est statique : aucun serveur, aucune base de données, aucune étape de build obligatoire.

### Méthode 1 — Déploiement via interface Vercel

1. Créer un repository GitHub avec le projet.
2. Aller sur [vercel.com](https://vercel.com).
3. Cliquer sur **Add New Project**.
4. Importer le repository.
5. Laisser les paramètres par défaut :
   - Framework Preset : `Other` ;
   - Build Command : vide ;
   - Output Directory : vide ou racine du projet.
6. Cliquer sur **Deploy**.

### Méthode 2 — Déploiement via CLI

Installer Vercel CLI :

```bash
npm i -g vercel
```

Déployer :

```bash
vercel
```

Déployer en production :

```bash
vercel --prod
```

---

## ⚙️ Fichier `vercel.json`

Le projet contient un fichier minimal :

```json
{
  "cleanUrls": true,
  "trailingSlash": false,
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        }
      ]
    }
  ]
}
```

Il sert à :

- activer des URLs propres ;
- éviter les slashs finaux inutiles ;
- ajouter un header de sécurité simple.

---

## 🎨 Direction artistique

Le design s’inspire du drapeau camerounais :

```txt
Vert → Rouge → Jaune
```

Avec une étoile jaune placée sur la partie rouge dans les visuels principaux.

Principes visuels :

- interface sombre par défaut ;
- cartes Liquid Glass ;
- effets de flou et transparence ;
- dégradés camerounais ;
- animations légères ;
- compatibilité `prefers-reduced-motion` ;
- responsive mobile-first.

---

## 🔐 Confidentialité et stockage

Le site utilise :

- `localStorage` pour la langue et le thème ;
- `sessionStorage` pour afficher la popup WhatsApp une seule fois par session ;
- la géolocalisation navigateur si l’utilisateur accepte ;
- une API IP publique en fallback approximatif ;
- EmailJS pour envoyer les propositions d’entreprise.

Aucune donnée n’est stockée dans une base de données côté serveur.

---

## ✅ Checklist avant mise en production

- [ ] Remplacer `EMAILJS_TEMPLATE_ID` dans `assets/js/contact-form.js`.
- [ ] Ajouter le vrai lien affilié 1xBet dans le bloc publicitaire.
- [ ] Vérifier les numéros et adresses des entreprises.
- [ ] Ajouter d’autres villes : Bafoussam, Bamenda, Garoua, Kribi, Limbe.
- [ ] Optimiser ou remplacer les images externes si nécessaire.
- [ ] Tester le partage du lien sur WhatsApp, Facebook, LinkedIn et X/Twitter.
- [ ] Tester le rendu mobile Safari et Chrome Android.

---

## 📌 Pages disponibles

| Page | Rôle |
|---|---|
| `index.html` | Accueil, présentation, villes disponibles |
| `entreprises.html` | Carte, liste, recherche, filtres, formulaire |
| `documentation.html` | Guide d’utilisation et d’extension |
| `mentions-legales.html` | Informations légales |
| `confidentialite.html` | Politique de confidentialité |

---

## 👤 Crédit

**CONGLOMERAT**  
Crazy Prince Dev — Fullstack 2026  
Made with 💜 from Cameroon 🇨🇲  
WhatsApp : [+237694268225](https://wa.me/237694268225)
