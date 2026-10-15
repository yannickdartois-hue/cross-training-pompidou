# ✕ Cross Training Pompidou

> Application EPS hors-ligne pour piloter les séances de Cross Training au Lycée Georges Pompidou (Castelnau-le-Lez).  
> Un seul fichier HTML — aucune installation, aucun serveur, aucun compte.

**[▶ Lancer l'application](https://yannickdartois-hue.github.io/cross-training-pompidou/)**

---

## Présentation

Application PWA single-file conçue pour les tablettes iPad et Android utilisées en gymnase.  
Elle gère le profil des élèves, les WODs minutés avec chrono, les niveaux de reps, les notes d'exécution et le bilan en QR code scannable par le professeur.

---

## 5 modes WOD

| Mode | Description | Durée |
|------|-------------|-------|
| **AMRAP** | Autant de tours que possible | 7–20 min |
| **For Time** | Terminer le circuit le plus vite possible | Chrono montant |
| **TABATA** | 20″ effort / 10″ repos × 8 cycles | 4 min |
| **EMOM** | Un exercice chaque début de minute | 4–8 min |
| **EMOM+1** | EMOM avec exercice bonus en fin de minute | 4–8 min |

---

## Fonctionnalités principales

### Côté élève
- Saisie du profil (nom, prénom, classe)
- Chrono dédié par mode avec phases effort/repos animées
- Compteur de reps par tap — niveaux N0 (4 reps) à N4 (12 reps)
- Notes d'exécution par exercice (1–5)
- Ressenti WOD et ressenti séance (étoiles + smiley + commentaire)
- **Mode binôme** : une tablette, deux élèves, alternance avec passage de tablette
- Bilan final avec QR code compact (≈ 161 bytes, Level M)

### Côté professeur
- Vue tableau des élèves avec recherche et filtrage par classe
- **Scan QR code** : import instantané du bilan élève (BarcodeDetector natif + fallback photo iOS)
- Double bip + vibration au scan réussi
- Export CSV complet (24 colonnes, séparateur `;`, BOM UTF-8 Excel)
- Filtrage par classe avant export
- Détection de doublons avec choix Remplacer / Annuler

### Exercices et niveaux
- 3 exercices par WOD parmi une bibliothèque organisée par filière et zone
- Filières : 🤸 Gainage (violet) · 🏋️ Endurance (bleu) · 🔥 Intensif (orange)
- Zones : Haut du corps → Tronc & Abdos → Bas du corps
- Reps cibles adaptées au niveau : N0 = 4 · N1 = 6 · N2 = 8 · N3 = 10 · N4 = 12

---

## Format QR code

Un QR code par élève (ou par élève en mode binôme) encode la séance complète :

```
NOM;PRENOM;CLASSE;SCORE_WOD1;EX:exo1,exo2,exo3;NE:note1,note2,note3;LV:niveau;D:duree;RW:resWod|SCORE_WOD2;...;R:resSeance:commentaire
```

**Exemple :**
```
FONTANY;Francois;TLE PRO;A:N1-3t=18r;EX:PLACON,DISQU,JUMJA;NE:3,4,2;LV:1;D:7;RW:4:Sympa|E:7/10;EX:SQUAT,BURPE,GAINOU;NE:4,3,5;LV:2;D:8;RW:3;R:4:Bonne séance
```

---

## Export CSV professeur — 24 colonnes

`Nom · Prénom · Classe · Coach · WOD n° · WOD total · Mode · Durée · Score · Niveau · Exo1 · Note1 · Exo2 · Note2 · Exo3 · Note3 · Ressenti WOD note · Ressenti WOD · Commentaire WOD · Ressenti séance note · Ressenti séance · Commentaire séance · Heure · Date`

---

## Compatibilité

| Plateforme | Statut |
|------------|--------|
| iPad Safari (iOS 16+) | ✅ Testé |
| Samsung Galaxy Tab 8 (Chrome) | ✅ Testé |
| Android Chrome générique | ✅ Compatible |
| Desktop Chrome / Firefox | ✅ Compatible |
| Installation PWA (icône accueil) | ✅ Supporté |

> **iOS Safari** : `confirm()` remplacé par modals custom, canvas QR hors-écran, fallback photo pour le scan.

---

## Utilisation

1. Ouvrir `https://yannickdartois-hue.github.io/cross-training-pompidou/` sur la tablette
2. (Optionnel) Ajouter à l'écran d'accueil pour l'utiliser hors-ligne
3. Saisir le profil élève ou passer en **Vue Prof** pour le tableau de classe

Aucune connexion requise après le premier chargement.

---

## Déploiement

Le projet est un fichier HTML unique (`index.html`) déployé via GitHub Pages.

Pour mettre à jour l'application :
1. Aller sur le dépôt GitHub
2. **Add file → Upload files → index.html → Commit changes**
3. GitHub Pages redéploie en quelques secondes

---

## Structure technique

```
index.html  (~500 KB)
├── Block 0 : QRCode.js (génération QR)
├── Block 1 : jsQR webpack bundle (scan QR)
└── Block 2 : Application complète
    ├── CSS variables + thèmes clair/sombre
    ├── HTML sections (accueil, WOD, bilan, prof)
    └── JS : STATE, BINOME, PROF, fonctions WOD
```

**Dépendances** : aucune externe — tout est inliné dans le fichier HTML.

---

## Auteur

**Yannick Dartois** — Professeur d'EPS  
Lycée Polyvalent Georges Pompidou · Castelnau-le-Lez · Académie de Montpellier

---

*Application développée pour un usage pédagogique interne. Libre de droits pour les établissements scolaires.*
