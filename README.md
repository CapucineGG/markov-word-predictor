# Markov Word Predictor

Prédicteur de mots en JavaScript basé sur des chaînes de Markov, entraîné sur un corpus de textes littéraires français (Gutenberg).

## Description

Ce projet implémente un système de prédiction de mots entraîné sur un corpus de textes littéraires français (Gutenberg).

Il propose trois modes de prédiction :

- **Compléter le mot** : suggère les mots les plus fréquents qui commencent par les lettres saisies
- **Prédire le mot suivant (Markov ordre 1)** : à partir d'un seul mot, prédit les mots les plus probables qui viennent juste après dans les textes
- **Prédire le mot suivant avec contexte (Markov ordre 2)** : à partir de deux mots consécutifs, prédit le mot suivant le plus probable ; ce mode donne des résultats plus cohérents car il prend en compte le contexte

## Prérequis

- [Node.js](https://nodejs.org/) ≥ 18

## Installation

```bash
git clone https://github.com/CapucineGG/markov-word-predictor.git
cd markov-word-predictor
npm install
```

## Utilisation

### 1. Générer les fichiers de données

```bash
npm run dic    # Génère dictionnaire.json
npm run pred   # Génère predictions.json
npm run pred2  # Génère predictions2.json
```

### 2. Tester les modèles

```bash
npm run testdic   # Lance le script de démonstration du dictionnaire
npm run testpred  # Lance le script de démonstration prédiction ordre 1
npm run testpred2 # Lance le script de démonstration prédiction ordre 2
```

### Exemple de sortie

<!-- Coller un exemple de sortie comme testpred2 -->

```
Paire 'il est' :
[ ... résultat réel à coller ici ... ]
```

## Structure du projet

```
markov-word-predictor/
├── data/           # Corpus source (.txt) et fichiers générés (.json)
├── src/
│   ├── creation_*.js     # Génération du dictionnaire et des modèles de prédiction
│   ├── fonction_utile.js # Fonctions utilitaires (nettoyage de texte, écriture JSON)
│   └── demo_*.js         # Scripts de démonstration
├── package.json
└── README.md
```


## Détails techniques

### Dictionnaire de fréquences (dictionnaire.json)

Création d'un dictionnaire à partir de tous les mots du corpus. Chaque mot est associé à une fréquence (entre 0 et 1) qui indique à quel point il apparaît souvent dans les textes.

### Modèle de Markov : ordre 1 (predictions.json)

Pour chaque mot, on regarde quels mots peuvent venir juste après dans les textes. On enregistre ces mots avec leur fréquence (normalisée entre 0 et 1).

On utilise une boucle `for` classique pour construire le dictionnaire, car c'est beaucoup plus rapide que Ramda sur de gros volumes de données.

### Modèle de Markov : ordre 2 (predictions2.json)

Pour chaque paire de mots consécutifs, on regarde quel mot peut venir juste après dans les textes. On enregistre ces mots avec leur fréquence (normalisée entre 0 et 1).

La clé du dictionnaire est une chaîne `"mot1 mot2"`, ce qui permet de prédire le mot suivant en fonction des deux mots précédents plutôt qu'un seul. Cela permet d'intégrer un contexte dans la prédiction.

Pour les mêmes raisons que l'ordre 1, on utilise une boucle `for` au lieu de Ramda.

### Nettoyage du texte

Avant de traiter les textes, on les nettoie :
- Suppression des parties inutiles (en-têtes et pieds de page du Projet Gutenberg)
- Passage en minuscules
- Suppression de la ponctuation et des caractères spéciaux
- Découpage en mots

## Corpus utilisés

- Jules Lemaître, *Petits Contes*
- *Fables* de La Fontaine
- Maupassant, *Contes du jour et de la nuit*

(Textes du domaine public, issus du [Projet Gutenberg](https://www.gutenberg.org/))

## Limites et axes d'amélioration

- Les prédictions sont limitées au vocabulaire du corpus d'entraînement (littérature classique du XIXe siècle)
- Pas de lissage statistique (smoothing) pour les paires de mots rares
- Piste future : interface web pour tester les prédictions sans exécuter le code

## Licence

Ce projet est sous licence MIT — voir le fichier [LICENSE](LICENSE).

## Auteur

**Capucine Gombert-Gillmann** — [GitHub](https://github.com/CapucineGG)
