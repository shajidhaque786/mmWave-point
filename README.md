# mmWave Person Identification

This project investigates person identification using millimetre-wave (mmWave) radar point clouds. It evaluates classical machine-learning and deep-learning approaches and examines how the choice of train/test split affects reported performance.

The Jupyter notebook contains the revised experiment, including data processing, model evaluation, and result visualisations. The project compares random splitting with a block-based split that uses guard bands to reduce leakage between nearby, potentially overlapping temporal windows.

## Research question

Does randomly splitting overlapping temporal windows produce an overly optimistic estimate of person-identification performance compared with a block split that separates neighbouring observations?

## Project contents

```text
.
├── README.md
├── mmwave_identification_revised.ipynb
├── raw/                       # Local dataset; obtain separately
│   ├── 0.pkl ... 18.pkl
│   ├── action_label.npy
│   └── id.json
└── results/
    ├── figures/               # Generated plots (PNG and PDF)
    └── model_comparison/
        └── notebook_results.csv
```

The raw data files are not included in GitHub. See [`raw/README.md`](raw/README.md) for how to obtain and place them.

## Dataset

The project uses the MiliPoint mmWave radar point-cloud dataset. Download the dataset from [Google Drive](https://drive.google.com/file/d/1rq8yyokrNhAGQryx7trpUqKenDnTI6Ky/view) and place the required files in the `raw/` directory at the project root. The notebook expects the data in that location; see its data-loading cells if your local folder layout differs.

Expected files include session files `0.pkl` through `18.pkl`, plus `id.json` and `action_label.npy` where required by the notebook. Keep the downloaded data private if you do not have permission to redistribute it.

## Requirements

The notebook uses Python and common scientific Python packages. Depending on which cells you run, install:

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install numpy pandas scikit-learn matplotlib jupyter torch
```

PyTorch installation options can depend on your operating system and hardware. Use the [official PyTorch installation selector](https://pytorch.org/get-started/locally/) if the simple `pip install torch` command is not suitable.

## Run the notebook

1. Download and extract the dataset into `raw/`.
2. Install the required packages.
3. Start Jupyter from the project directory:

   ```bash
   jupyter notebook
   ```

4. Open `mmwave_identification_revised.ipynb` and run the cells in order.

The complete experiment may take substantial time and memory. Start with the notebook's smaller demonstration settings before running the full analysis.

## Evaluation and metrics

The experiment compares random and block-based evaluation protocols. Random splits can place highly similar or overlapping neighbouring windows in both training and test sets, which may inflate performance. Block splits use contiguous temporal partitions and guard bands to reduce this risk.

Reported measures and visualisations include accuracy-based and class-balanced metrics, model comparisons, confusion matrices, and per-class results, as produced by the notebook.

## Results

Figures and notebook result summaries are stored under `results/`. The checked-in results represent one run and may depend on the dataset version, settings, and random seed. Record these details when reporting or reproducing results.

## Reproducibility checklist

For a reproducible final run, record the dataset version, participant/session counts, notebook settings, random seeds, evaluation protocol, Python version, and key package versions. Run the notebook from top to bottom with the dataset arranged as described above.

## Project summary

This project studies how accurately individuals can be identified from mmWave radar point clouds. It compares classical and deep-learning methods and focuses on whether temporal overlap between windows can cause information leakage and overly optimistic evaluation. Results should be interpreted alongside the split protocol used.

