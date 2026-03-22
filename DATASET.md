# Dataset Documentation — P5 Generative AI

## Primary Dataset: OASIS-1 (Marcus et al., 2007)

| Attribute | Value |
|---|---|
| Full name | Open Access Series of Imaging Studies — Phase 1 |
| Source | https://www.oasis-brains.org |
| Access | Free registration required |
| Subjects | 416 (aged 18–96; healthy + Alzheimer's disease) |
| Modality | T1-weighted MRI (1.5T MPRAGE) |
| Slices used | Central 30 axial slices per subject (~12,480 total) |
| Image size | 128 × 128 px, grayscale, normalised [0, 1] |
| Licence | Public domain for non-commercial research |

**Citation:**
> Marcus, D. S., Wang, T. H., Parker, J., Csernansky, J. G., Morris, J. C., & Buckner, R. L. (2007).
> Open Access Series of Imaging Studies (OASIS): Cross-sectional MRI data in young, middle aged,
> nondemented, and demented older adults.
> *Journal of Cognitive Neuroscience, 19*(9), 1498–1507.

---

## Phantom Fallback (for reproducible execution)

If `./oasis_slices/` is absent, the notebook **automatically activates** `USE_PHANTOM = True`
and generates synthetic MRI-like phantom images via `generate_phantom_mri()`.

This ensures the notebook runs **top-to-bottom without errors** on any machine,
without requiring OASIS download or registration.

To use real OASIS data:
1. Register at https://www.oasis-brains.org
2. Download OASIS-1 NIfTI volumes
3. Extract central 30 axial slices per subject as 128×128 PNG files
4. Place all PNG files in `./oasis_slices/`
5. Set `USE_PHANTOM = False` in the notebook (Cell 4)

---

## Why OASIS-1 was chosen

- Real, peer-reviewed, publicly available neuroimaging data (not synthetic, not AI-generated)
- Clinically relevant: spans healthy aging and Alzheimer's disease pathology
- Not reused from any prior Nanodegree project (P2: Wine CSV; P3: Iris; P4: Fashion-MNIST)
- Directly relevant to the dementia AI research context motivating this project
