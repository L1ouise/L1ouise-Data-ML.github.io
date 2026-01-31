---
layout: default
title: "Classification de races de chiens — Deep Learning"
---

#  Classification de races de chiens  
### Deep Learning & Computer Vision — Stanford Dogs Dataset

##  Objectif du projet
Développer un modèle capable d’identifier automatiquement la race d’un chien à partir d’une image, en utilisant le **Stanford Dogs Dataset** (20 000+ images, 120 races).  
Ce projet illustre ma capacité à gérer un dataset complexe, construire un CNN performant et optimiser un pipeline ML complet.

---

#  1. Compréhension du dataset & défis techniques

###  Dataset : Stanford Dogs
- 20 580 images haute résolution  
- 120 races très proches visuellement  
- Classification fine-grained (textures, formes, couleurs subtiles)

###  Défis principaux
- Forte variabilité des images  
- Classes visuellement proches  
- Dataset déséquilibré  
- Risque d’overfitting élevé  

---

#  2. Préparation & augmentation des données

###  Prétraitement
- Normalisation  
- Redimensionnement  
- Split train/validation/test  

###  Data augmentation
Pour améliorer la généralisation :

- rotations  
- zoom  
- shear  
- flips horizontaux  
- translations  

 Résultat : un dataset enrichi, plus robuste, limitant le surapprentissage.

---

#  3. Construction du modèle CNN

###  Architecture personnalisée
- **Conv2D + MaxPooling**  
- **GlobalAveragePooling**  
- **Dropout** (régularisation)  
- **Dense (120 classes)** avec softmax  

###  Pourquoi ce choix ?
- Architecture légère mais expressive  
- Adaptée à la classification fine  
- Compatible GPU Kaggle (Tesla T4)

---

#  4. Entraînement & optimisation

###  Hyperparamètres
- Batch size optimisé (32–64)  
- Learning rate dynamique  
- Optimizer : Adam  

###  Callbacks avancés
- **ModelCheckpoint** : sauvegarde du meilleur modèle  
- **ReduceLROnPlateau** : réduction automatique du LR  
- **EarlyStopping** : arrêt intelligent  

###  Entraînement GPU
- GPU Tesla T4 (Kaggle)  
- Entraînement accéléré et plus stable  

---

#  5. Résultats & performances

###  Métriques suivies
- Accuracy  
- Top‑5 accuracy  
- Loss / val_loss  

###  Résultats obtenus
- **Accuracy : ~38%**  
- **Top‑5 accuracy : >74%**  
- **Val loss minimale : 2.63**

 Pour un modèle **from scratch** sur un dataset aussi difficile, ce sont d’excellents résultats.

---

#  6. Analyse & interprétation

###  Analyse des courbes
- Détection du surapprentissage  
- Ajustement du learning rate  
- Stabilisation progressive  

###  Insights
- Le modèle apprend bien les motifs globaux  
- Les races proches restent difficiles (normal pour du fine-grained)  
- La data augmentation améliore fortement la top‑5 accuracy  

---

#  7. Fonction de prédiction

Fonction permettant :

- de charger une image  
- de la prétraiter  
- de prédire la race  
- d’afficher les **5 races les plus probables**  

 Fonction essentielle pour une démo ou une application réelle.

---

#  Compétences démontrées

###  Deep Learning
CNN, optimisation, fine-grained classification

###  Computer Vision
Prétraitement d’images, data augmentation, interprétation

###  MLOps / Workflow ML
Pipeline complet, sauvegarde & chargement de modèles, analyse des métriques

###  Outils
TensorFlow / Keras, OpenCV, Kaggle GPU, Python (NumPy, Pandas, Matplotlib)

---

#  Lien GitHub
 *(Ajoute ici le lien vers ton repo du projet)*

---

#  Retour aux projets
[← Voir tous les projets](/projets)
