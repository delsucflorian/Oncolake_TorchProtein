# OncoLake-TorchProtein

Comparing handcrafted structural features to learned geometric embeddings
for oncogene vs tumor suppressor classification.

This project extends [OncoLake](https://github.com/SDK-Bmd/Oncolake),
which used a Random Forest on 25 features extracted from AlphaFold-predicted
protein structures. The original model did not outperform a majority-class
baseline (CV accuracy 0.53 vs 0.56). A review of its feature set shows that
only one feature out of 25 (radius of gyration) encodes actual 3D geometry;
the rest are sequence-derived or reflect prediction confidence. The
structural hypothesis was not really tested.

This project tests it with a Graph Neural Network
([TorchProtein](https://torchprotein.ai)) applied directly to the atomic
graph of each protein.

## Research question

Three protein representations are compared under the same evaluation
protocol:

1. Amino acid composition only (sequence baseline)
2. Composition + AlphaFold global descriptors (OncoLake baseline)
3. GNN-learned geometric embeddings (TorchProtein)

Three outcomes are pre-declared:

- Learned embeddings significantly outperform both baselines. Structural
  signal exists locally and is recoverable by representation learning.
- All three converge. Structural signal is not present at the level of the
  isolated protein; discrimination requires additional modalities
  (interactome, expression, tissue context).
- Composition alone suffices. Structural information adds nothing over the
  amino acid distribution.

## Methodological changes from OncoLake original

- Family-aware split instead of stratified random split, to prevent paralog
  leakage between train and test.
- F1 macro instead of accuracy, given the class imbalance (225 oncogenes,
  179 tumor suppressors).
- A single evaluation pipeline shared by all three models (same splits,
  same seeds, same metrics) for fair comparison.

## Status

In development, September 2026.

- [x] Research question defined
- [x] OncoLake data imported (manifest, .cif, reference features)
- [ ] Evaluation pipeline (family-aware split, F1 macro)
- [ ] OncoLake baseline reproduction with corrected methodology
- [ ] TorchProtein embedding extraction
- [ ] Classifier training on learned embeddings
- [ ] Final comparison and interpretability (permutation importance, SHAP)
- [ ] Final report

## Repository structure

```
oncolake-torchprotein/
├── data/
│   ├── manifest.json                    # 418 proteins, frozen
│   ├── features_baseline_ref.parquet    # OncoLake reference features (404 × 25)
│   ├── metrics_baseline_ref.json        # OncoLake reference metrics
│   └── SOURCE_NOTE.md                   # data provenance
├── notebooks/
├── src/
├── results/
├── requirements.txt
└── README.md
```

The 409 AlphaFold `.cif` files (~2 GB) are not included in the repo. See
[`data/SOURCE_NOTE.md`](data/SOURCE_NOTE.md) for provenance.

## Reproducibility

The dataset is frozen and not regenerated from UniProt or AlphaFold during
this project, so that results remain strictly comparable to the OncoLake
baseline. Provenance is documented in
[`data/SOURCE_NOTE.md`](data/SOURCE_NOTE.md).

## Results

To be added.

## References

- OncoLake — [SDK-Bmd/Oncolake](https://github.com/SDK-Bmd/Oncolake), 2025.
- Zhu et al., *TorchDrug: A Powerful and Flexible Machine Learning
  Platform for Drug Discovery*, 2022.
  [arXiv:2202.08320](https://arxiv.org/abs/2202.08320).
- Jumper et al., *Highly accurate protein structure prediction with
  AlphaFold*, Nature, 2021.
- The UniProt Consortium, *UniProt: the Universal Protein Knowledgebase
  in 2023*, Nucleic Acids Research, 2023.

## Author

Florian Delsuc, ING3 EFREI (Big Data & Machine Learning), 2026.
Contact: delsuc.florian@gmail.com

## License

MIT — see [LICENSE](LICENSE).
