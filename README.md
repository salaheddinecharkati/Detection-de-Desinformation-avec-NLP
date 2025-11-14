# Detection-de-Desinformation-avec-NLP

---

## 📝 Introduction

La désinformation représente aujourd'hui un défi majeur, en particulier sur les réseaux sociaux où les fake news se propagent rapidement et influencent l'opinion publique.  
Ce projet s'inscrit dans le champ du traitement automatique du langage naturel (NLP) et vise à développer un système de détection automatique de fausses informations basé sur l'utilisation du modèle BERT.  
L'objectif est de proposer une approche efficace permettant d'identifier des articles douteux et d'assister les efforts de vérification des faits.

---

## 🎯 Objectifs et champ d'application

- Détecter automatiquement les fake news à partir d'articles textuels.
- Fournir une aide à la vérification des faits pour les journalistes et chercheurs.
- Expérimenter l'utilisation d'un modèle pré-entraîné BERT pour la classification de texte.

---

## 🤖 Présentation du modèle BERT

BERT (Bidirectional Encoder Representations from Transformers) est un modèle NLP développé par Google.  
- Architecture basée sur les Transformers.  
- Lecture **bidirectionnelle** des séquences de texte pour une compréhension fine du contexte.  
- Pré-entraîné sur une grande quantité de données textuelles.  
- Adaptable à des tâches spécifiques comme la classification de texte.  

Dans ce projet, BERT est utilisé pour différencier les fake news des articles fiables.

---

## 📊 Données utilisées

### ISOT Fake and Real News Dataset
- Contenu : environ 44 000 articles répartis en deux classes : FAKE et REAL.  
- Fichiers : `Fake.csv` (fausses informations) et `True.csv` (informations vérifiées).  
- Colonnes principales : `title`, `text`, `subject`, `date`.  
- Une colonne `label` a été ajoutée pour la classification (`0 = FAKE`, `1 = REAL`) et encodée avec `LabelEncoder`.

### Prétraitement des textes
- Utilisation du tokenizer BERT.
- Troncature et padding à une longueur maximale de 128 tokens.
- Génération des `input_ids` et `attention_mask`.
- Séparation des données :
  - Train : 80%
  - Validation : 10%
  - Test : 10%
- Stratification selon les classes.

---

## ⚙️ Méthodologie

### Entraînement du modèle
- Modèle : `BertForSequenceClassification` (`num_labels=2`)
- Entraînement avec la classe `Trainer` de Hugging Face.
- Hyperparamètres :
  - Époques : 4
  - Batch size : 16
  - Optimiseur : AdamW
- Sélection du meilleur modèle selon le **F1-score**.

### Évaluation du modèle
- Métriques calculées : accuracy, précision, rappel, F1-score.
- Résultats sur le jeu de test :
  - Loss : 0.0032
  - Accuracy : 99.95%
  - Precision : 100%
  - Recall : 99.91%
  - F1-score : 99.95%

### Matrice de confusion
|            | Prédit FAKE | Prédit REAL |
|------------|------------|------------|
| Réel FAKE  | 2348       | 0          |
| Réel REAL  | 2          | 2140       |

- Accuracy : 99.96%

---

## ✅ Conclusion

Le projet démontre qu'un modèle BERT bien entraîné peut détecter efficacement les fake news avec une précision élevée.  
Cette approche peut être intégrée dans des systèmes d'alerte automatisés pour limiter la propagation de la désinformation sur les plateformes numériques.
