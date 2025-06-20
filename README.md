# Translation Demo - Projet d’Évaluation de Modèles de Traduction Automatique

## 1. Introduction

Ce projet vise à comparer les performances de plusieurs modèles de traduction automatique pour la paire de langues Anglais → Français.  
Il s’appuie sur un dataset benchmark avec textes originaux en anglais et leurs références de traduction en français.

Les modèles testés sont :  
- 2 modèles Hugging Face : Helsinki-NLP (MarianMT) et mBART (facebook/mbart-large-50-many-to-many-mmt)  
- 2 modèles Ollama : LLaMA 3.2 et Mistral 7B

Nous évaluons leur qualité de traduction à différents niveaux de **température** (0, 0.2, 0.5, 0.8, 1.0), qui contrôle la créativité / diversité des sorties.

---

## 2. Dataset utilisé

Nous avons utilisé un extrait du dataset **WMT14 English-French** disponible sur Hugging Face (`wmt14`) contenant des phrases anglaises originales et leurs traductions françaises de référence.  
Cela permet une évaluation objective avec des métriques standards.

---

## 3. Méthodologie

- **Modèles Hugging Face** chargés via `transformers` (MarianMT et mBART)  
- **Modèles Ollama** intégrés via appels système à leur API locale  
- Pour chaque modèle, traduction des phrases avec 5 températures différentes  
- Calcul des scores **BLEU** et **ROUGE-L** sur un échantillon test (10 phrases)

---

## 4. Résultats d’évaluation (10 phrases test)

| Modèle                  | Température | BLEU  | ROUGE-L |
| ----------------------- | ----------- | ----- | ------- |
| **Helsinki (HF)**       | 0.0         | 31.01 | 0.586   |
|                         | 0.2         | 30.00 | 0.570   |
|                         | 0.5         | 24.70 | 0.561   |
|                         | 0.8         | 25.84 | 0.560   |
|                         | 1.0         | 19.04 | 0.506   |
| **mBART (HF)**          | 0.0         | 26.65 | 0.549   |
|                         | 0.2         | 30.64 | 0.560   |
|                         | 0.5         | 24.59 | 0.535   |
|                         | 0.8         | 12.53 | 0.388   |
|                         | 1.0         | 8.00  | 0.304   |
| **LLaMA 3.2 (Ollama)**  | 0.0         | 11.17 | 0.469   |
|                         | 0.2         | 7.32  | 0.260   |
|                         | 0.5         | 3.23  | 0.155   |
|                         | 0.8         | 2.62  | 0.169   |
|                         | 1.0         | 3.06  | 0.137   |
| **Mistral 7B (Ollama)** | 0.0         | 19.14 | 0.475   |
|                         | 0.2         | 14.95 | 0.392   |
|                         | 0.5         | 10.00 | 0.304   |
|                         | 0.8         | 5.11  | 0.241   |
|                         | 1.0         | 6.21  | 0.254   |

---

## 5. Explication des métriques

### BLEU (Bilingual Evaluation Understudy)  
Mesure la similarité entre la traduction et la référence en comparant les n-grammes. Score entre 0 (mauvais) et 100 (parfait).

### ROUGE-L (Longest Common Subsequence)  
Évalue la qualité en fonction de la plus longue sous-séquence commune entre traduction et référence, reflétant la cohérence globale.

---

## 6. Démo interactive

L’application Gradio fournie permet de tester en direct les 4 modèles avec les températures paramétrables.  
L’interface offre :  
- Saisie d’un texte en anglais  
- Choix du modèle et de la température  
- Affichage instantané de la traduction française

---

## 7. Instructions pour lancer le projet

```bash
git clone https://github.com/Merwan6/translation-demo.git
cd translation-demo
python -m venv venv
source venv/bin/activate  # ou venv\Scripts\activate sous Windows
pip install -r requirements.txt
python main.py
```

---

## 8. Configuration des modèles Ollama

Pour utiliser les modèles locaux LLaMA 3.2 et Mistral 7B via Ollama :

1. Installez Ollama : https://ollama.com/

2. Téléchargez les modèles avec :

```bash
ollama run llama3
ollama run mistral
```

```bash
OLLAMA_LLAMA_MODEL=llama3
OLLAMA_MISTRAL_MODEL=mistral
```

```bash
OLLAMA_PATH=ton/chemin/vers/modele
```

---

## 9. Vidéo démo

Une démonstration courte du fonctionnement de l’application est disponible dans le dépôt :  
📽️ [Voir la vidéo de démonstration](./assets/videos/demo_traduction.mp4)

---

## 10. Structure du projet

translation-demo/
├── main.ipynb
├── README.md
├── requirements.txt
├── .gitignore
├── assets/
│ └── videos/
│ └── demo_traduction.mp4