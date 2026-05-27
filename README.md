# CRISPR-Cas9 p53 replacement for cancer therapy

Project repository for a computational pipeline that generates cancer-type-specific CRISPR-Cas9 sgRNA panels for the **non-hotspot** (70%) fraction of TP53 somatic missense mutations in ovarian, pancreatic, and colorectal cancer cohorts.

## Layout

```
.
├── code/                   # Python pipeline (import-ready modules + CLI)
│   ├── crispr_p53/         # library
│   ├── main.py             # CLI
│   ├── README.md           # code-level docs
│   └── requirements.txt
├── data/                   # (fill with cached cBioPortal / NCBI pulls if desired)
├── figures/                # PNG figures (regenerated on every run)
├── paper/                  # full academic write-up (.docx)
├── results/                # CSVs + summary.json (regenerated on every run)
└── README.md               # this file
```

## Quick start

```bash
cd code
pip install -r requirements.txt
python main.py --mode demo         # offline demo cohort
# or:
python main.py --mode live         # live cBioPortal PanCancer Atlas
```

The pipeline writes CSVs to `../results/`, figures to `../figures/`, and a full summary to `../results/summary.json`.

## Paper

The full methodology, results, and discussion are in
[`paper/TP53_sgRNA_prioritization_paper.docx`](paper/TP53_sgRNA_prioritization_paper.docx).

## What this pipeline finds

On the matched ovarian / pancreatic / colorectal demo cohorts (300 samples each):

- **~96% sgRNA coverage** of unique non-hotspot missense positions with composite score ≥ 0.75.
- **Two reproducible PAM-desert positions** (C238, V274) that cannot be targeted with SpCas9 within a ±10 nt edit window in any cohort.
- **Consensus sgRNAs** that cover clusters of adjacent non-hotspot mutations simultaneously (e.g. one spacer covers I255 / L257 / E258).
- **Cancer-type-specific supplements**: colorectal surfaces three unique C-terminal regulatory-domain targets (e.g. E336) that are invisible to ovarian/pancreatic-derived panels.

## License

Research code. Cite the paper and the underlying public datasets (TCGA PanCancer Atlas, IARC TP53 Database, Doench et al. 2016) if you build on this.
