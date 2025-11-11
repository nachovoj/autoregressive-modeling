# Autoregressive-Modeling

This repository presents a **fully reproducible analytical workflow** implementing a classical **autoregressive (AR)** modeling approach.\

It introduces the mathematical and computational foundations behind AR parameter estimation using **linear algebra (Toeplitz matrices)** and **statistical inference (Yule–Walker equations)**.

------------------------------------------------------------------------

## 1) Project Overview and Objectives

### Global Objective

Develop and document a **transparent, reproducible, and mathematically grounded** approach to estimating autoregressive model parameters using linear algebra and statistical inference.

### Specific Analytical Steps

-   Build the **core matrix formulation** behind AR(p) models.
-   Estimate **autoregressive coefficients** using the Yule–Walker approach.
-   Compare **manual vs. optimized (SciPy)** implementations.
-   Validate results through **empirical estimation (OLS)** and **benchmark performance**.

------------------------------------------------------------------------

## 2) Analytical Summary

The workflow integrates both mathematical reasoning and computational validation:

| Stage | Component | Description |
|------------------|------------------|------------------------------------|
| **1** | **Manual Toeplitz Construction** | Build a Toeplitz matrix from an input vector to visualize its structure. |
| **2** | **Optimized Implementation** | Use SciPy’s optimized `toeplitz()` for efficient computation. |
| **3** | **Validation & Error Handling** | Introduce explicit input checks to ensure robustness and reproducibility. |
| **4** | **Performance Benchmarking** | Compare execution speed between manual and optimized routines. |
| **5** | **Autoregressive Parameter Estimation** | Estimate AR(p) parameters from the covariance structure and validate results against OLS estimation. |

The notebook follows strict reproducibility and documentation standards — ensuring that each result can be regenerated from scratch.

------------------------------------------------------------------------

## 3) Prerequisites

| Tool | Purpose | Installation |
|------------------|-----------------------|-------------------------------|
| **Quarto (≥ 1.5)** | Render and document the notebook | [quarto.org/docs/get-started](https://quarto.org/docs/get-started) |
| **Python (≥ 3.10)** | Run the analysis | [python.org/downloads](https://www.python.org/downloads/) |
| **Jupyter** | Kernel backend for Quarto | `pip install jupyter` |
| **TinyTeX** *(optional)* | For PDF rendering | `quarto install tinytex` |

### 3.1 Verify installation

#### Windows (PowerShell)

``` powershell
python --version
pip --version
jupyter --version
quarto check
```

#### macOS / Linux (Terminal)

```         
python3 --version
pip3 --version
jupyter --version
quarto check
```

If any command fails, install the missing component from the links above.

### 3.2 PDF Rendering

If rendering to PDF, install **TinyTeX** (lightweight LaTeX distribution):

```         
quarto install tinytex
quarto check 
```

### 3.3 Recommended IDEs

| Tool | Compatibility | Notes |
|------------------------|------------------------|------------------------|
| **VS Code** (with Quarto extension) | Full | Recommended for editing and rendering |
| **Positron IDE** | Full | Native support for Quarto and Python execution |
| **Terminal / PowerShell** | Full | Use `quarto render <file>.qmd` |

### 3.4 Dependencies

The `requirements.txt` file includes:

-   **numpy**, **scipy**, **pandas** – numerical and matrix operations
-   **statsmodels** – autoregressive model estimation
-   **matplotlib** – residual and diagnostic plots
-   **pathlib**, **timeit** – reproducibility and performance benchmarking

------------------------------------------------------------------------

## 4) Repository Structure

The repository follows a clean, modular structure ensuring clarity and reproducibility in Python.

```         
autoregressive-modeling/
├── data/                   # Input data (e.g., vector.csv)
├── notebooks/              # Quarto source file
│   └── Toeplitz_YuleWalker.qmd
├── reports/                # Rendered outputs (HTML or PDF)
├── requirements.txt        # Python dependencies
├── .gitignore              # Cache, envs, and temporary files
└── README.md               # Project documentation
```

**Highlights**

-   Modular and reproducible structure.

-   All paths defined dynamically with `pathlib` for cross-platform compatibility.

-   Outputs generated automatically during rendering

> **Note:** Figures and data outputs are generated dynamically during notebook execution.

## 4) Repository Structure

```         
autoregressive-modeling/
├── data/                   # Input data (e.g., vector.csv)
├── notebooks/              # Quarto source file
│   └── Toeplitz_YuleWalker.qmd
├── reports/                # Rendered outputs (HTML or PDF)
├── requirements.txt        # Python dependencies
├── .gitignore              # Cache, environments, and temp files
└── README.md               # Project documentation
```

> **Note:** Figures and data outputs are generated dynamically during notebook execution.

------------------------------------------------------------------------

### Execution Tip

When working with **Positron** or **VS Code**, always open the **entire project folder** (not individual files).\
This ensures that relative paths, the virtual environment (`.venv`), and Quarto rendering all function correctly.

``` bash
# Example of correct workflow
File → Open Folder → select the project root (e.g., autoregressive-modeling/)
```

If the terminal starts in a subdirectory (like `/notebooks/`), relative paths to `/data/` or `/reports/` may fail.

------------------------------------------------------------------------

## 5) Running the Project

### 5.1 Environment Setup

**Windows (PowerShell):**

```         
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt 
```

**macOS / Linux:**

```         
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

### 5.2 Rendering the Notebooks

Render using Quarto:

```         
quarto render notebooks/Toeplitz_YuleWalker.qmd --to html --output-dir ../reports 
```

To produce a PDF report:

```         
quarto render notebooks/Toeplitz_YuleWalker.qmd --to pdf --output-dir ../reports 
```

Rendered outputs are stored automatically under `/reports/`.

------------------------------------------------------------------------

## 6) Expected Results

-   A validated **Toeplitz matrix** construction (manual and optimized).
-   Estimated **AR(p) coefficients** using Yule–Walker equations.
-   Consistency check with **OLS estimates** from `statsmodels.AutoReg`.
-   Performance metrics comparing both implementations.
-   Residual plots confirming model adequacy.

These results confirm that the manually implemented Toeplitz matrix and the Yule–Walker estimation are both correct and consistent with library-based OLS methods — demonstrating analytical accuracy and computational efficiency.

------------------------------------------------------------------------

## 7) Reproducibility Principles

-   **Transparency** – All parameters and assumptions visible in code blocks.

-   **Modularity** – Each section can run independently.

-   **Cross-platform compatibility** – Dynamic path detection.

-   **Performance awareness** – Benchmarking between manual and library methods.

-   **Clear validation** – Numerical equivalence tested with `np.allclose()`.

------------------------------------------------------------------------

## 8) Key Analytical Foundations

| Concept | Description |
|------------------------------------|------------------------------------|
| **Toeplitz Matrix** | A structured matrix with constant diagonals, fundamental in time series covariance representation. |
| **Yule–Walker Equations** | Linear system linking autocovariances to AR coefficients. |
| **Autoregressive (AR) Models** | Predict current values of a series from past observations. |
| **Performance Benchmarking** | Quantifies computational efficiency across implementations. |

------------------------------------------------------------------------

## 9) Troubleshooting

| Issue | Possible Cause | Recommended Solution |
|------------------|-----------------------|-------------------------------|
| **PDF render fails** | Missing or incomplete LaTeX installation | Install TinyTeX via `quarto install tinytex`, or render to HTML instead. |
| **Kernel not found** | Python environment not linked to Jupyter | Run `python -m ipykernel install --user --name=.venv`. |
| **ModuleNotFoundError** | Missing Python package | Run `pip install -r requirements.txt`. |
| **File not found (`vector.csv`)** | Working directory incorrect | Ensure `data/vector.csv` exists or adjust the relative path in the notebook. |
| **Execution stops midway** | Cached state or memory overflow | Restart the Quarto daemon: `quarto render --execute-daemon-restart`. |

------------------------------------------------------------------------

## 10) Author

**Ignacio Vélez Ocampo**\
*MSc Management – Business Analytics*\
Focused on integrating analytics, automation, and reproducible workflows for data-driven insights.

------------------------------------------------------------------------

*All content, code, and documentation are original and fully reproducible.*
