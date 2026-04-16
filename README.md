# eLiga SN — Championnat Pro Club FC26

Dashboard statique de gestion du championnat eLiga SN · Saison 1 · 16 équipes · 30 journées.

---

## Déploiement sur Netlify

### Option 1 — Via l'interface Netlify (recommandé)

1. Va sur [netlify.com](https://netlify.com) et connecte-toi
2. Clique sur **"Add new site" → "Deploy manually"**
3. Glisse-dépose le dossier `FC26_championat/` dans la zone de dépôt
4. Le site est en ligne en moins d'une minute

### Option 2 — Via GitHub

1. Crée un dépôt GitHub et pousse le projet :
   ```bash
   git init
   git add .
   git commit -m "Initial deploy eLiga SN"
   git remote add origin https://github.com/TON_USER/eliga-sn.git
   git push -u origin main
   ```
2. Sur Netlify : **"Add new site" → "Import an existing project"**
3. Connecte ton dépôt GitHub
4. Paramètres de build :
   - **Build command** : *(laisser vide)*
   - **Publish directory** : `.`
5. Clique sur **"Deploy site"**

### Option 3 — Via Netlify CLI

```bash
npm install -g netlify-cli
netlify login
netlify deploy --dir . --prod
```

---

## Structure du projet

```
FC26_championat/
├── index.html              # Dashboard principal (seul fichier servi)
├── assets/
│   ├── logo_eLiga_Sn.jpg   # Logo de la ligue
│   └── Blacksquad.png      # Logo équipe Blacksquad
├── netlify.toml            # Configuration Netlify (cache, headers)
├── _redirects              # Règles de redirection SPA
├── equipes/                # Fiches équipes (.md)
├── matchs/                 # Résultats de matchs (.md)
├── classement/             # Classement actuel (.md)
├── stats/                  # Statistiques buteurs/passeurs (.md)
├── regles/                 # Règlement du championnat (.md)
└── saisons/                # Programmation des journées (.md)
```

---

## Dépendances externes

| Ressource | Usage | Statut |
|-----------|-------|--------|
| Google Fonts (Bebas Neue, Rajdhani) | Typographie | CDN Google — en ligne uniquement |

> Toutes les images et ressources visuelles sont locales dans `assets/`.

---

## Mise à jour du site

Le dashboard est un fichier HTML statique. Pour mettre à jour les données :
- Modifier `index.html` directement
- Redéployer via Netlify (drag & drop ou `git push`)

---

## Gestion du championnat

Voir [CLAUDE.md](CLAUDE.md) pour les instructions complètes de gestion des matchs, classements et statistiques.
