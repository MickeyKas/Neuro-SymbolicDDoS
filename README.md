├── NeuroSymbolicIDS.ipynb # Main Jupyter notebook with full pipeline, training, evaluation, and figures
├── README.md # This file
├── requirements.txt # Python dependencies
└── outputs/ # Folder where results (tables, figures, models) are saved (created automatically)

text

## Datasets

We evaluate on three publicly available benchmark datasets:

| Dataset        | # Features | # Attack Types | Imbalance | Preprocessing |
|----------------|------------|----------------|-----------|----------------|
| CIC‑DDoS2019   | 78         | 12             | High       | Undersample training to 30% attacks |
| Edge‑IIoTset   | 44         | 15 (OT/IIoT)   | Balanced   | No down‑sampling |
| CICIoT23       | 46         | Various DDoS   | High       | Undersample training to 30% attacks |

## Requirements

- Python 3.11+
- PyTorch 2.1.0 (CPU build – the model runs entirely on CPU)
- scikit‑learn 1.3.0
- pandas, numpy, matplotlib, seaborn, tqdm

Install all dependencies with:

```bash
pip install -r requirements.txt
Usage
Clone the repository and navigate into it.

Prepare the datasets (see below for expected folder structure).

Run the Jupyter notebook:

bash
jupyter notebook NeuroSymbolicIDS.ipynb
The notebook will:

Load and preprocess the three datasets.

Train the GRU and decision tree models.

Perform grid search over α and τ on validation sets.

Evaluate the hybrid model on test sets.

Generate all figures (bar charts, confusion matrices, ROC/PR curves, training curves, heatmaps).

Save results and figures in the outputs/ directory.

Expected Dataset Folder Structure
Place the datasets under F:\jupyter\kagglehub\ (or modify the paths in cell 2 of the notebook).

text
F:\jupyter\kagglehub\
├── datasets\dhoogla\cicddos2019\versions\3\          # CIC-DDoS2019 (multiple .parquet files)
├── edgeiiotset-cyber-security-dataset-of-iot-iiot\versions\5\Edge-IIoTset dataset\Selected dataset for ML and DL\   # Edge-IIoTset (.csv)
└── CICIOT23\                                           # CICIoT23 (train.csv, validation.csv, test.csv)
If your paths differ, adjust the BASE_PATH variable in the notebook.

Results Summary
Dataset	Model	Accuracy (%)	F1 (%)	FNR (%)	Latency (ms)
CIC‑DDoS2019	Pure Neural	96.91	97.98	3.34	0.76
Pure Symbolic	70.08	77.82	32.12	0.58
Hybrid	99.04	99.38	0.67	0.79
Edge‑IIoTset	Pure Neural	99.32	98.90	0.76	0.79
Pure Symbolic	100.00	100.00	0.00	0.65
Hybrid	100.00	100.00	0.00	0.80
CICIoT23	Pure Neural	97.87	98.90	2.16	0.58
Pure Symbolic	76.08	86.04	24.50	0.55
Hybrid	98.61	99.29	1.22	0.62
Note: Hybrid latency is the maximum of the two individual latencies plus a small overhead for fusion.

Optimised Fusion Parameters
Dataset	α (neural weight)	τ (threshold)	Validation F1 (%)
CIC‑DDoS2019	0.725	0.475	99.35
Edge‑IIoTset	0.000	0.050	100.00
CICIoT23	0.950	0.050	99.29
Figures Generated
The notebook produces the following figures (saved in outputs/):

bar_*.pdf/png – Bar charts for accuracy, F1, ROC‑AUC, PR‑AUC, FPR, FNR.

confusion_matrices.pdf/png – Row‑normalised confusion matrices for the hybrid model.

roc_curves.pdf/png – ROC curves with AUC.

pr_curves.pdf/png – Precision‑recall curves with AP.

training_curves.pdf/png – GRU training loss and validation F1 over epochs.

alpha_heatmap_*.pdf/png – Validation F1 heatmaps over α and τ.

neuro_symbolic_results_full.csv – Full test results table.

confusion_matrix_summary.csv – Raw confusion matrix counts.

Reproducibility
All random seeds are fixed (seed = 42) for deterministic results. The preprocessing pipeline is fully automated. The code is self‑contained in a single Jupyter notebook.

Citation
If you use this code or our methods in your research, please cite our paper:

bibtex
@article{alemayehu2026neuro,
  title={A Neuro-Symbolic Framework for DDoS Detection in Resource-Constrained Operational Technology, PLC, ICS, and SCADA Environments},
  author={Alemayehu, Mikiyas and Ghanem, Mohamed Chahine and Kheddar, Hamza},
  journal={arXiv preprint},
  year={2026}
}
License
This project is licensed under the MIT License – see the LICENSE file for details.

Contact
For questions or issues, please open an issue on GitHub or contact the corresponding author.

Mohamed Chahine Ghanem – mohamed.chahine.ghanem@liverpool.ac.uk

text

You can save this as `README.md` in your repository root. It includes all necessary sections, results tables, usage instructions, and a clear description of the project.
