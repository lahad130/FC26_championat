# Méthode — Traitement des performances et résultats

## 1. Réception des screenshots

L'utilisateur dépose les images dans :
`/Users/toure/FC26_championat/assets/performances/`

Lire chaque image avec le tool `Read` pour extraire :
- Le score final (écran "Détails du match" ou score en haut)
- La note générale de l'équipe
- Le meilleur joueur (⭐ Player of the Match)
- Le tableau des joueurs avec leurs notes (NR), buts (B) et passes décisives (PD)

---

## 2. Ce qu'on extrait par match

Pour chaque match (aller ET retour séparément) :

| Info | Où la trouver |
|------|--------------|
| Score | Écran "Détails du match" ou bandeau en haut |
| MOTM | Joueur avec ⭐ dans le tableau de performances |
| Buteurs | Colonne B > 0 |
| Passeurs | Colonne PD > 0 |
| Note | Chiffre dans le cercle en haut à droite du joueur |

---

## 3. Créer le fichier match MD

Chemin : `matchs/match_J{N}_{EQ1}_vs_{EQ2}.md`
Pour le retour : `matchs/match_J{N}_retour_{EQ1}_vs_{EQ2}.md`

Template :
```markdown
# Match J{N} — {Équipe 1} vs {Équipe 2} (Aller/Retour)

- **Journée** : {N}
- **Date** : YYYY-MM-DD

## Score

| Équipe 1 | Score | Équipe 2 |
|----------|-------|----------|
| {Nom}    |  X–Y  | {Nom}    |

## Meilleures performances

| Équipe | ⭐ Meilleur joueur | Note |
|--------|-------------------|------|
| {Nom}  | {Joueur} ⭐        | X.X  |
| {Nom}  | {Joueur}          | X.X  |

## Buteurs

- {Joueur} ({Équipe}) ×{nb}

## Passeurs décisifs

- {Joueur} ({Équipe}) ×{nb}
```

---

## 4. Mises à jour dans index.html (via Python)

### Classement (standings tbody)
- Recalculer PJ, V, N, D, BP, BC, Diff, Pts pour chaque équipe
- Trier par : Pts > Diff > BP
- Or = 1er, Argent = 2e, Bronze = 3e, reste = muted

### Onglet Résultats
- Ajouter une card cliquable par match :
  `onclick="openMatchModal('id-du-match')"`
- Afficher score, résumé buteurs en bas de card

### Objet MATCHES (JS)
Ajouter une entrée :
```js
'id-du-match': {
  label: 'Aller/Retour · Journée N',
  eq1: 'Nom', logo1: 'assets/logo.webp',
  score: 'X – Y',
  eq2: 'Nom', logo2: 'assets/logo.webp',
  buteurs: ['Joueur ×N (Équipe)', ...],
  passeurs: ['Joueur ×N (Équipe)', ...]
}
```

### Onglet Buteurs
- Retrier TOUS les buteurs de TOUTES les équipes (y compris les perdants) par total cumulé
- Barres proportionnelles au max (joueur #1 = 100%)
- Ne jamais oublier les buteurs des équipes qui ont perdu

### Onglet Passeurs
- Même logique que buteurs, toutes équipes confondues

### Tab Performance
- **Une seule liste classée par note décroissante** (pas séparée par match)
- Afficher uniquement : joueur, équipe, note
- Pas de détail du match, pas de mention "aller/retour"

### Sidebar Derniers Résultats
- Afficher TOUS les matchs joués de la journée (pas seulement 3)
- Trier du plus récent au plus ancien

### Sidebar Top Buteurs
- Top 5 mis à jour avec tous les buteurs de tous les matchs joués

### Section sous classement
- Ajouter les nouvelles cards de résultats (cliquables)

### Calendrier
- Mettre les scores joués, badge "✅ Terminée"

---

## 5. Cas particuliers

- **Double forfait** : PJ+2, V+1, D+1 pour chaque équipe, score 3-0. Pas de buteurs/passeurs.
- **Joueur inconnu** : mettre "À compléter" en attendant confirmation
- **Une seule perf reçue** : noter l'équipe manquante comme "non envoyée", mettre quand même les infos disponibles
- **Xalatt Niakk** : pas de performances envoyées (ils perdent tout), normal
- **Équipes perdantes** : inclure quand même leurs buteurs et passeurs dans les classements

---

## 6. Outils utilisés

- **Read** : lire les screenshots JPG/PNG
- **Write** : créer les fichiers .md
- **Python `str.replace()`** : modifier les gros blocs HTML (Edit échoue sur trop grands blocs)
- **Edit** : modifications ciblées petites
