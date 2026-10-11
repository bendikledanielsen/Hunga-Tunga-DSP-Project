# Hunga Tonga — Digital Signal Processing

Python analysis of atmospheric infrasound recorded following the January 2022 Hunga Tonga–Hunga Haʻapai volcanic eruption. This university coursework project combines signal processing, visualisation and arrival-time analysis using recordings from **201 stations**.

**Start here:** [Analysis notebook](Hunga_Tunga_DSP.ipynb) · [PDF report](Hunga_Tunga_DSP.pdf) · [HTML export](Hunga_Tunga_DSP.html)

## Methods

- Loaded HDF5 station recordings and calculated great-circle distances from the eruption.
- Implemented discrete convolution and a sampled discrete-time Fourier transform (DTFT) using explicit summation, with small examples to check their outputs.
- Examined the frequency responses of three supplied FIR filters and identified low-pass, band-pass and high-pass behaviour.
- Applied the filters to all 201 recordings using NumPy convolution.
- Visualised station locations, filter responses and signals as a function of time and distance.
- Built an interactive workflow to select wave arrival times and save selections across multiple sessions.
- Estimated propagation celerity using linear regression and compared two residual-based outlier thresholds.

## Results

The stations span approximately **2,138–17,687 km** from Hunga Tonga. Regression of manually selected arrival times against distance produced the following estimates:

| Outlier threshold | Excluded recordings | Estimated celerity |
| --- | ---: | ---: |
| One standard deviation of the initial fit residuals | 27 | 278.14 m/s |
| Two standard deviations of the initial fit residuals | 12 | 264.25 m/s |

These are exploratory estimates. Their sensitivity to outlier selection, together with uncertainty in manual arrival picks, limits their precision. The notebook includes plots, interpretation and references.

## My contribution and supplied material

My work includes the convolution and DTFT implementations, filter-response analysis, filtering and visualisation, interactive arrival-time selection, regression analysis and written interpretation.

The project builds on supplied course material: the MATLAB script `run_provided.m`, FIR filter coefficients in `impulse_response.txt`, and Python parsing and mapping snippets shared by **Markus Bjørklund**. Attribution is retained in the notebook. These supplied components are distinguished from my own implementations and analysis.

## Repository contents

| File | Purpose |
| --- | --- |
| `Hunga_Tunga_DSP.ipynb` | Main notebook with code, plots and explanations |
| `Hunga_Tunga_DSP.pdf` | Exported report for reading without running the code |
| `Hunga_Tunga_DSP.html` | HTML export of the notebook |
| `bjorklund_extracts.py` | Supplied Python helper snippets |
| `run_provided.m` | Supplied MATLAB reference script |
| `impulse_response.txt` | Coefficients for the three FIR filters |
| `picks_session*.npz` | Saved manual arrival-time selections |

## Running the notebook

### 1. Clone the repository

```bash
git clone https://github.com/bendikledanielsen/Hunga-Tunga-DSP-Project.git
cd Hunga-Tunga-DSP-Project
```

### 2. Install dependencies

Python 3 and the following packages are required:

```bash
python -m pip install numpy matplotlib h5py python-dateutil cartopy geopy jupyter
```

Using a virtual environment is recommended.

### 3. Provide the recordings

The original HDF5 recordings are **not included in this repository**. The notebook expects them in a `data/` directory at the repository root. Obtain the recordings from the original course data source before running the full analysis.

The parser expects station latitude and longitude attributes, waveform data under a `/waveforms` group, and waveform `starttime` and `delta` attributes. It is configured for 720,000 samples per station.

You can read the saved notebook outputs or PDF report without obtaining the dataset.

### 4. Open the notebook

From the repository root, run:

```bash
jupyter notebook Hunga_Tunga_DSP.ipynb
```

Run the analysis cells in order. The manual arrival-picking section uses `plt.ginput()` and currently selects the macOS Matplotlib backend with `%matplotlib osx`. On other systems, choose a supported interactive GUI backend. Running the picking cells again will overwrite the corresponding saved session files; skip those cells to reuse the included selections after loading and processing the original recordings.

## Author

**Bendik Le Danielsen** — Electronics, Informatics and Technology student at the University of Oslo.

This repository documents an educational project. Supplied code and data remain subject to their original terms; no additional reuse licence is granted here.
