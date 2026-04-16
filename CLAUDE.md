# FC26 Pro Club - Championnat

## Contexte du projet

Gestion d'un championnat FC26 Pro Club avec 12 équipes. Ce fichier contient toutes les règles, conventions et instructions pour gérer la compétition.

---

## Structure du projet

```
FC26_championat/
├── CLAUDE.md                        # Ce fichier — règles et contexte
├── equipes/                         # Fiche de chaque équipe
│   ├── equipe_01.md
│   ├── ...
│   └── equipe_12.md
├── matchs/                          # Données brutes des matchs
│   └── match_JJJJ_EQ1_vs_EQ2.md
├── classement/                      # Classements générés
│   └── classement_actuel.md
├── stats/                           # Statistiques joueurs et équipes
│   ├── buteurs.md
│   └── passeurs.md
├── regles/                          # Règlement du championnat
│   └── reglement.md
└── saisons/
    └── saison_1/
        ├── journees/                # Programmation des journées
        └── resultats/               # Résultats par journée
```

---

## Format des équipes

Chaque fichier dans `equipes/` suit ce format :

```markdown
# Nom de l'équipe

- **Abréviation** : ABC
- **Capitaine** : Pseudo
- **Joueurs** : Pseudo1, Pseudo2, ... (max 11)
- **Couleur** : Rouge/Blanc
```

---

## Format des matchs

Chaque fichier dans `matchs/` suit la convention de nommage :
`match_J{num_journee}_{EQ1}_vs_{EQ2}.md`

Contenu :

```markdown
# Match J{N} — {Équipe 1} vs {Équipe 2}

- **Journée** : {N}
- **Date** : YYYY-MM-DD
- **Heure** : HH:MM

## Score

| Équipe 1 | Score | Équipe 2 |
|----------|-------|----------|
| {Nom}    |  X-Y  | {Nom}    |

## Buteurs

- {Pseudo} ({Équipe}) — {minute}'
- ...

## Passeurs décisifs

- {Pseudo} ({Équipe}) — assist pour {Buteur}
```

---

## Règles du championnat

### Format de compétition
- **16 équipes**, championnat en matchs aller-retour = **30 journées**
- Chaque équipe joue **2 fois** contre chaque adversaire (1 à domicile, 1 à l'extérieur)
- 8 matchs par journée

### Système de points
| Résultat | Points |
|----------|--------|
| Victoire | 3 pts  |
| Nul      | 1 pt   |
| Défaite  | 0 pt   |

### Critères de départage (en cas d'égalité au classement)
1. Différence de buts générale
2. Nombre de buts marqués
3. Confrontations directes (points, puis diff. buts, puis buts marqués)
4. Fair-play (moins de cartons)

### Fin de saison
- **1er** : Champion — Badge Champion
- **2e et 3e** : Vice-champions
- **14e, 15e, 16e** : Zone de relégation (avertissement ou exclusion selon règlement)

---

## Instructions pour Claude

### Quand on te donne des résultats de matchs
1. Enregistrer le match dans `matchs/match_J{N}_{EQ1}_vs_{EQ2}.md`
2. Mettre à jour le classement dans `classement/classement_actuel.md`
3. Mettre à jour `stats/buteurs.md` et `stats/passeurs.md`
4. Indiquer si la journée est complète et afficher le classement mis à jour

### Quand on te demande le classement
- Lire tous les fichiers de matchs joués
- Calculer : PJ, V, N, D, BP, BC, Diff, Pts
- Afficher un tableau trié par points (puis critères de départage)

### Quand on programme une journée
- Créer le fichier dans `saisons/saison_1/journees/journee_{N}.md`
- Vérifier qu'aucune équipe ne joue deux fois dans la même journée
- Respecter l'alternance domicile/extérieur sur la saison

### Conventions de nommage
- Noms d'équipes : toujours utiliser le nom officiel du fichier `equipes/`
- Journées : J1 à J22
- Dates : format ISO `YYYY-MM-DD`

---

## État actuel

- **Saison** : 1
- **Équipes** : 16
- **Journées jouées** : 0 / 30
- **Dernière mise à jour** : 2026-03-31
