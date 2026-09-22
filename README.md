[README (1).md](https://github.com/user-attachments/files/32502286/README.1.md)
# Kernel PCA on Olivetti Faces — M2RG20 Group Coursework

This repository presents the **Olivetti Faces experiments from our M2RG20 Kernel Method group coursework, completed in June 2026 at Imperial College London**. It explores how different kernels affect dimensionality reduction, face classification, and image reconstruction.

This focused repository is maintained by Nathan Chen, whose contribution to the group project centred on Kernel PCA. It retains the collaborative context of the original coursework and credits the group contributors for their work.

**Original group repository:** [Deuter1um/M2RG20-Kernel-Method](https://github.com/Deuter1um/M2RG20-Kernel-Method)

## Overview

The experiments compare linear Principal Component Analysis (PCA) with Kernel PCA using RBF, polynomial, sigmoid, and cosine kernels. A k-nearest neighbours classifier evaluates the resulting representations, while reconstruction experiments examine how much image information can be recovered from the reduced features.

The notebook investigates:

- Linear PCA, cumulative explained variance, and eigenfaces.
- Kernel hyperparameter selection through cross-validation.
- Classification using raw pixels, PCA features, and Kernel PCA features.
- Two-dimensional embeddings and sensitivity to the number of components and RBF bandwidth.
- Image reconstruction, mean squared error, and regularisation of the approximate inverse mapping.
- Kernel similarity matrices and their centred eigenvalue spectra.

## Dataset

The **Olivetti Faces** dataset contains 400 grayscale images of 40 people, with 10 images per person. Each image has a resolution of 64 × 64 pixels, giving 4,096 input features.

The notebook loads the dataset with scikit-learn's `fetch_olivetti_faces()`. The first run requires an internet connection to download the data; subsequent runs use the local cache. The dataset itself is not included in this repository.

## Experimental setup

| Setting | Coursework configuration |
| --- | --- |
| Train/test split | Stratified 80/20 split: 320 training images and 80 test images |
| Random seed | 42 |
| Main representation size | 200 components |
| Classifier | kNN with 5 neighbours |
| Kernel parameter selection | 5-fold cross-validation on the training set |
| Classification metric | Accuracy |
| Reconstruction metric | Mean squared error (MSE) |

For classification grid search, Kernel PCA and kNN are combined in a pipeline, so the dimensionality reduction is fitted separately within each cross-validation fold.

## Recorded coursework results

The following classification accuracies are taken from the original notebook's saved outputs, using 200 components and the kernel parameters selected by cross-validation.

| Representation | Test accuracy |
| --- | ---: |
| Linear PCA | 82.5% |
| RBF Kernel PCA | 82.5% |
| Polynomial Kernel PCA | 83.8% |
| Sigmoid Kernel PCA | 86.2% |
| Cosine Kernel PCA | 86.2% |

These results describe one split of a small dataset. They do not establish that Kernel PCA consistently outperforms linear PCA. With 80 test images, one additional correct prediction changes accuracy by 1.25 percentage points. The numbers above have not been independently rerun for this repository draft.

## Running the notebook

Create a Python virtual environment and install the notebook dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install numpy scipy matplotlib scikit-learn jupyterlab
python -m jupyterlab
```

On Windows, activate the environment with `.venv\Scripts\activate` instead.

Open `notebooks/olivetti_kernel_pca.ipynb` and run the cells in order. Grid searches and reconstruction sweeps may take some time. Exact numerical results and compatibility depend on the installed package versions; a validated, pinned environment is not yet provided.

## Repository contents

| File or directory | Purpose |
| --- | --- |
| `notebooks/olivetti_kernel_pca.ipynb` | Main Olivetti experiment and analysis |
| `README.md` | Project background, methods, and running instructions |

The notebook is adapted from `kernel_pca_olivetti .ipynb` in the original group repository. Experiments involving MNIST, COIL-20, and financial market data are outside the scope of this repository.

## Interpretation and limitations

The original notebook includes exploratory component and bandwidth sweeps evaluated on the test set. Its reconstruction studies also select inverse-map parameters using test-set MSE. Those selected reconstruction errors should be read as exploratory results, rather than independent estimates of generalisation performance. A follow-up evaluation should select all such parameters on training/validation data and reserve the test set for final scoring.

The 2D embeddings are descriptive plots fitted on a subset of the full dataset, not held-out classification evaluations. Kernel PCA reconstruction is an approximate pre-image calculation; it does not provide directly viewable eigenfaces in the same way as linear PCA.

## Acknowledgements

Thanks to the contributors to the original **M2RG20 Kernel Method group project**. This repository preserves and presents part of that shared coursework. It also relies on the Olivetti Faces dataset and the NumPy, SciPy, Matplotlib, and scikit-learn projects.
