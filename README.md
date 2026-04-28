# Transformers_Fine_Tuning_Bart

Fine-tuning du modèle **BART** (encoder-decoder de Facebook) pour la tâche de **résumé automatique de dialogues**, sur le dataset [DialogSum](https://huggingface.co/datasets/knkarthick/dialogsum).

## Principe du projet

L'objectif est de spécialiser un modèle Transformer pré-entraîné généraliste (`facebook/bart-base`) sur un domaine précis : la synthèse de dialogues conversationnels. La démarche suit cinq étapes :

1. **Chargement du dataset** DialogSum (12 460 dialogues d'entraînement, 1 500 de test) depuis Hugging Face.
2. **Baseline** : test du modèle pré-entraîné `facebook/bart-large-cnn` pour avoir un point de comparaison.
3. **Tokenisation** des dialogues et résumés avec `AutoTokenizer` (max 128 tokens, padding, masque d'attention, labels à `-100` sur le padding).
4. **Fine-tuning** de `bart-base` via la classe `Trainer` de Hugging Face — 3 époques, learning rate 5e-5, weight decay 0.01, warmup 500 steps.
5. **Évaluation comparative** avec la métrique **ROUGE** (ROUGE-1, ROUGE-2, ROUGE-L) entre le modèle pré-entraîné et le modèle fine-tuné.

## Résultats

Sur 100 dialogues du test set, le modèle fine-tuné est **2 à 3× meilleur** que le pré-entraîné :

| Métrique | Pré-entraîné | Fine-tuné |
|----------|--------------|-----------|
| ROUGE-1  | 0.16         | **0.33**  |
| ROUGE-2  | 0.03         | **0.10**  |
| ROUGE-L  | 0.12         | **0.25**  |

Qualitativement, les résumés générés par le modèle fine-tuné sont plus concis, mieux structurés et fidèles au contenu du dialogue.

## Contenu du dépôt

- `Transformers.ipynb` — notebook complet (préparation des données, entraînement, évaluation).
- `Presentation Bart.pptx` — **présentation détaillée** du projet : architecture BART, méthodologie, concepts techniques (embeddings, attention, tokenisation, weight decay), résultats quantitatifs et qualitatifs.

Pour plus de clarifications sur le choix de l'architecture, les concepts techniques mobilisés et l'analyse des résultats, se référer à la présentation.
