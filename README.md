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

| Modèle                | Température | BLEU  | ROUGE-L |
| --------------------- | ----------- | ----- | ------- |
| **HF Helsinki**       | 0.0         | 31.01 | 0.586   |
|                       | 0.2         | 27.54 | 0.563   |
|                       | 0.5         | 29.89 | 0.536   |
|                       | 0.8         | 14.93 | 0.437   |
|                       | 1.0         | 19.43 | 0.441   |
| **HF mBART**          | 0.0         | 26.65 | 0.549   |
|                       | 0.2         | 29.38 | 0.563   |
|                       | 0.5         | 20.78 | 0.504   |
|                       | 0.8         | 17.13 | 0.452   |
|                       | 1.0         | 10.67 | 0.390   |
| **Ollama llama3.2**   | 0.0         | 24.14 | 0.519   |
|                       | 0.2         | 20.26 | 0.490   |
|                       | 0.5         | 28.88 | 0.547   |
|                       | 0.8         | 21.39 | 0.436   |
|                       | 1.0         | 16.04 | 0.445   |
| **Ollama mistral:7b** | 0.0         | 21.43 | 0.458   |
|                       | 0.2         | 23.08 | 0.454   |
|                       | 0.5         | 25.70 | 0.512   |
|                       | 0.8         | 20.73 | 0.428   |
|                       | 1.0         | 20.69 | 0.488   |

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