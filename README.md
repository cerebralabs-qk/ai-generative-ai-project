# P5 — Generative AI Applications
## Variational Autoencoder for Synthetic Brain MRI Generation

**Udacity Machine Learning Engineer Nanodegree**
**Author:** Qeis Kamran | GitHub: [cerebralabs-qk](https://github.com/cerebralabs-qk)

---

## Project Summary

This project implements a **Convolutional Variational Autoencoder (CVAE)** trained on
axial brain MRI slices from the OASIS-1 neuroimaging dataset. The model learns a
compressed probabilistic latent representation of T1-weighted MRI images and generates
novel synthetic brain slices by sampling from the learned latent distribution.

**Clinical motivation:** Synthetic brain MRI generation directly addresses data scarcity
in dementia AI pipelines — enabling privacy-preserving data augmentation for early
Alzheimer's detection systems.

---

## Submission Files

| File | Description |
|---|---|
| `generative_model.ipynb` | Main Jupyter notebook — runs top-to-bottom |
| `Generative_AI_Analysis_Report.pdf` | Full analysis and ethics report (13 pages, 21 references) |
| `requirements.txt` | Reproducibility file |
| `DATASET.md` | Dataset documentation (OASIS-1) |

---

## Model Architecture

| Component | Specification |
|---|---|
| Type | Convolutional VAE (Kingma & Welling, 2013) |
| Encoder | 4 × Conv2d (stride=2, LeakyReLU, BatchNorm) → μ, log σ² |
| Latent dim | 128 |
| Decoder | FC → 4 × ConvTranspose2d (stride=2, ReLU, BatchNorm) → Sigmoid |
| Loss | ELBO = BCE reconstruction + KL divergence (β=1) |
| Optimiser | Adam (lr=1e-3) + ReduceLROnPlateau |
| Training | 40 epochs, batch size 32, gradient clipping (max norm=1.0) |

---

## Quick Start

```bash
# 1. Clone
git clone https://github.com/cerebralabs-qk/ai-generative-ai-project.git
cd ai-generative-ai-project

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run notebook
jupyter notebook generative_model.ipynb
# Kernel → Restart & Run All
```

> **Note:** No OASIS data download required. The notebook auto-detects the
> absence of `./oasis_slices/` and activates the built-in MRI phantom generator
> for fully reproducible execution. See `DATASET.md` for real OASIS setup.

---

## Key Results

- Generated samples exhibit coherent brain morphology: oval skull boundary,
  white/grey matter contrast gradient, bilateral symmetry, ventricle regions
- Smooth latent space interpolation confirms a well-structured learned manifold
- Training converges stably over 40 epochs with no mode collapse
- Known limitation: BCE loss causes over-smoothing of fine anatomical detail

---

## References

- Kingma, D. P., & Welling, M. (2013). Auto-encoding variational Bayes. *arXiv:1312.6114*
- Marcus, D. S. et al. (2007). OASIS. *Journal of Cognitive Neuroscience, 19*(9), 1498–1507
- Goodfellow, I. et al. (2014). Generative adversarial nets. *NeurIPS 27*
- Full reference list: see `Generative_AI_Analysis_Report.pdf`
