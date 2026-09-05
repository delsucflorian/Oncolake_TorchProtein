# OncoLake-TorchProtein

> Do learned geometric embeddings capture structural signal that handcrafted 
> AlphaFold features miss?

Extension of the [OncoLake](https://github.com/SDK-Bmd/Oncolake) project — 
replacing handcrafted structural features with learned graph-based 
representations for oncogene vs tumor suppressor classification.

## Motivation

The original OncoLake project trained a Random Forest classifier on 25 
features extracted from AlphaFold-predicted structures to distinguish 
oncogenes from tumor suppressors. The result was negative: the model did 
not outperform a majority-class baseline (CV accuracy ~0.53 vs 0.56).

However, a closer look at the feature set reveals that only **one** feature 
out of 25 (`radius_of_gyration`) truly encodes 3D geometry. The remaining 
features are either sequence-derived (amino acid composition, length) or 
meta-information about AlphaFold's prediction confidence (`plddt_mean`, 
`pct_low_confidence`). **The structural hypothesis was never truly tested.**

This project tests it frontally — using a Graph Neural Network 
([TorchProtein](https://torchprotein.ai)) that operates directly on the 
3D atomic topology of each protein.

## Research question

Three representations of the same protein are compared, using a rigorous 
family-aware split and imbalance-aware metrics (F1 macro):

1. **Amino acid composition only** — sequence-based baseline, no structure
2. **Composition + AlphaFold global descriptors** — OncoLake original baseline
3. **GNN-learned geometric embeddings** — TorchProtein contribution

Three pre-declared outcomes, all scientifically exploitable:

- **(a)** Learned embeddings significantly outperform both baselines → 
  structural signal exists locally and representation learning captures it.
- **(b)** All three methods converge → structural signal doesn't exist at 
  the level of the isolated protein; discrimination requires additional 
  modalities (interactome, expression, tissue context).
- **(c)** Sequence composition alone suffices → OncoLake over-engineered 
  the problem; the signal is in the amino acid distribution, not the fold.

## Methodological improvements over OncoLake original

- **Family-aware split** (instead of stratified random split) to prevent 
  paralog leakage between train and test.
- **F1 macro** (instead of accuracy) to properly evaluate performance 
  under class imbalance (225 oncogenes vs 179 tumor suppressors).
- **Same evaluation pipeline** applied to all three models — identical 
  splits, seeds, and metrics — for fair comparison.

## Project status

🚧 In active development — September 2026.

- [x] Question de recherche définie
- [x] Import des données OncoLake (manifest, .cif, features de référence)
- [ ] Pipeline d'évaluation (split famille + F1 macro)
- [ ] Reproduction baseline OncoLake avec méthodologie corrigée
- [ ] Extraction embeddings TorchProtein
- [ ] Entraînement classifieurs sur embeddings
- [ ] Comparaison finale + interprétabilité (permutation importance / Shapley)
- [ ] Rapport final

## Repository structure

```
oncolake-torchprotein/
├── data/                          # Fichiers légers versionnés
│   ├── manifest.json              # 418 protéines figées
│   ├── features_baseline_ref.parquet  # Features de référence (404 × 25)
│   ├── metrics_baseline_ref.json  # Métriques baseline originale
│   └── SOURCE_NOTE.md             # Provenance des données
├── notebooks/                     # Notebooks Colab
├── src/                           # Code réutilisable
├── results/                       # Figures et tables finales
├── requirements.txt
└── README.md
```

**Note :** les 409 fichiers `.cif` d'AlphaFold (~2 GB) ne sont pas dans le repo. 
Voir `data/SOURCE_NOTE.md` pour leur provenance et comment y accéder.

## Reproducibility

Data provenance is documented in [`data/SOURCE_NOTE.md`](data/SOURCE_NOTE.md). 
The dataset is **frozen** and not regenerated from UniProt/AlphaFold during 
this project, to ensure strict comparability with the OncoLake original 
baseline.

Requirements will be pinned in `requirements.txt` and setup instructions 
will be added as the project matures.

## Results

*To be added upon completion.*

## Citations

- **OncoLake original** — [SDK-Bmd/Oncolake](https://github.com/SDK-Bmd/Oncolake), 2025.
- **TorchProtein / TorchDrug** — Zhu et al., *TorchDrug: A Powerful and 
  Flexible Machine Learning Platform for Drug Discovery*, 2022. 
  [arXiv:2202.08320](https://arxiv.org/abs/2202.08320).
- **AlphaFold** — Jumper et al., *Highly accurate protein structure 
  prediction with AlphaFold*, Nature 2021.
- **UniProt** — The UniProt Consortium, *UniProt: the Universal Protein 
  Knowledgebase in 2023*, Nucleic Acids Research 2023.

## Author

Florian DELSUC, ING3 EFREI (Big Data & Machine Learning), 2026.  
Contact : delsuc.florian@gmail.com

## License

MIT — see [LICENSE](LICENSE).
