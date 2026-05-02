# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Research project on the geometry of compression in latent diffusion models. Current focus: estimating differential-geometric quantities (reach, curvature, local feature size) from noisy point cloud samples of manifolds embedded in high-dimensional ambient spaces.

## Environment Setup

Uses `uv` with Python 3.12.10 and a local `.venv`:

```bash
uv sync                     # install dependencies
source .venv/bin/activate   # activate venv
```

## Commands

```bash
# Lint
uv run ruff check .
uv run ruff format .

# Run notebooks
jupyter notebook experiments/

# Run main entry point
uv run python main.py
```

## Architecture

All active research lives in `experiments/` as Jupyter notebooks:

- **`01-reach-estimation.ipynb`** — Estimates the reach of a sphere embedded in high-dimensional ambient space (R^D). Uses the ratio `‖p−q‖² / (2 · dist_to_tangent_plane)` as a pointwise reach estimator, then studies how noise level σ and ambient dimension D affect accuracy.

- **`02-lfs-estimation.ipynb`** — Estimates curvature (and by extension local feature size) for ellipses and tori. Two estimation methods are compared throughout:
  - *Empirical (PCA)*: local PCA to recover the tangent/normal basis, then fit a degree-2 polynomial in local coordinates; curvature κ = 2|β₂|.
  - *Exact tangent*: uses the analytical normal to bypass PCA error as a baseline.
  - Later cells extend to tori in R^N (arbitrary ambient dimension) with interactive `ipywidgets` sliders for n, m, σ, h, a, N.

The `papers/` directory holds the theoretical references the experiments implement (reach estimation, manifold estimation, curvature rates).

`main.py` is a placeholder entry point; substantive code is in the notebooks.
