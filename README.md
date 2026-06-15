# 🏋️ Calisthénie — Bien lever les bases

Petite app **standalone, sans backend** pour démarrer le programme de calisthénie
(Phase 1). Elle aide à **savoir quoi faire** (circuit guidé + niveau actuel +
fiches techniques) et à **noter ses résultats** (reps/temps par tour, journal,
progression de niveaux).

- 100 % **hors-ligne** une fois ouverte (PWA, service worker).
- Toutes les données restent **sur l'appareil** (`localStorage`). Aucun serveur.
- Installable sur le téléphone via « **Ajouter à l'écran d'accueil** ».

## Utilisation

| Onglet | À quoi ça sert |
|---|---|
| **Séance** | Lance le circuit guidé : 6 exercices × 3 tours, minuteurs de repos (60 s entre exercices, 2 min entre tours), saisie des reps/temps réalisés. Chrono intégré pour les exercices en tenue (gainage, suspension, L-sit). |
| **Progression** | Niveau actuel de chaque exercice + critère de validation. Bouton « Valider → suivant » quand tu réussis le critère. |
| **Journal** | Historique des séances. Export/import JSON pour sauvegarder. |
| **Fiches** | Fiches techniques de tous les niveaux de chaque exercice. |

Le circuit et les 6 exercices (tractions, pompes, pistol squats, gainage, dips,
L-sit), leurs niveaux et critères de validation sont définis dans le tableau
`EXERCICES` au début du `<script>` de `index.html`.

### Modifier / ajouter un exercice ou un niveau

Tout est dans la constante `EXERCICES` de `index.html`. Un niveau :

```js
{ id:'t1', nom:'Tractions australiennes', type:'reps', cible:15,
  critere:'15 répétitions, presque à l’horizontale.',
  desc:'Consignes d’exécution…', opt:false }
```

- `type` : `'reps'` (répétitions) ou `'temps'` (secondes à tenir → active le chrono).
- `cible` : objectif chiffré du niveau.
- `critere` : texte affiché dans l'onglet Progression.
- `desc` : fiche technique.
- `opt` : `true` pour un niveau optionnel.

Pour ajouter une **Phase 2**, il suffit d'ajouter les niveaux suivants à chaque
exercice (ou de nouveaux exercices) dans `EXERCICES`. Après modification, pense à
incrémenter `CACHE` dans `sw.js` (ex. `calisthenie-v2`) pour rafraîchir le cache.

## Tester en local

```bash
python3 -m http.server 8000
# puis ouvrir http://localhost:8000
```

> Ouvrir `index.html` par double-clic (`file://`) fonctionne aussi, mais le mode
> hors-ligne (service worker) ne s'active qu'en `http(s)://`.

---

## 🚀 Déploiement (GitHub Pages)

L'app est à la **racine** de ce repo (le workflow `.github/workflows/pages.yml`
et les chemins relatifs en dépendent). À chaque push sur `main`, le workflow
**Deploy to GitHub Pages** reconstruit et publie le site.

URL : **https://pgrydbeck.github.io/calisthenie/**

Pages est configuré sur **Settings → Pages → Source : GitHub Actions**.

## 📱 Installer sur le téléphone
Ouvre l'URL dans Safari/Chrome → menu Partager → **Ajouter à l'écran d'accueil**.
L'app s'ouvre en plein écran et fonctionne hors-ligne.
