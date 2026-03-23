# blockchain-climate-framework

# Blockchain-Climate Data Framework: Real-World Validation

[![DOI](https://zenodo.org/badge/1082188576.svg)](https://doi.org/10.5281/zenodo.17429218)

Supporting code and data for: **"A proof-of-stake blockchain framework for transparent climate data verification"**

## Contents

- `notebooks/noaa_validation_analysis.ipynb` - Google Colab notebook implementing statistical anomaly detection and sensitivity analysis
- `notebooks/Fig_1.ipynb` - Code to generate Figure 1 (hourly temperature plot with flagged anomalies)
- `notebooks/Fig_2.ipynb` - Code to generate Figure 2 (three-layer architecture diagram)
- `data/noaa_984290_2024.txt` - NOAA ISD hourly temperature data (Manila, Philippines, Jan–Dec 2024)
- `results/anomalies.csv` - Detected anomalies output file
- `README.md` - This file

## Quick Start

### Run in Google Colab

1. Click here: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/tomheston/blockchain-ai-climate-framework/blob/main/notebooks/noaa_validation_analysis.ipynb)
2. Upload `noaa_984290_2024.txt` when prompted
3. Run all cells
4. Results export as `anomalies.csv`

### Run Locally

```bash
# Clone repository
git clone https://github.com/tomheston/blockchain-ai-climate-framework.git
cd blockchain-ai-climate-framework

# Open notebook in Jupyter
jupyter notebook notebooks/noaa_validation_analysis.ipynb
```

**Requirements:** Python 3.7+, pandas, numpy, matplotlib

## Method

Validates statistical anomaly detection using a global-baseline z-score method on real-world climate observations.

**Algorithm:**

1. Load hourly temperature data (8,408 records)
2. Remove NOAA-flagged erroneous values (coded −9999), yielding 8,403 valid observations
3. Convert temperatures from tenths of degrees Celsius to degrees Celsius
4. Compute global mean and standard deviation across the full dataset
5. Calculate z-scores for each observation: z = (x - μ) / σ
6. Flag anomalies where |z| > 3.0
7. Report detected events with timestamps, temperatures, and z-scores

**Sensitivity analysis:** The notebook also evaluates thresholds of |z| > 2.5 and |z| > 3.5 to assess the effect of threshold selection on anomaly detection.

## Data Source

**NOAA Integrated Surface Database (ISD)**

- Station: 984290-99999 (Manila Ninoy Aquino International Airport)
- Location: 14.5°N, 121.0°E
- Period: January 1 – December 31, 2024
- Total records: 8,408 (8,403 valid after QC)
- Completeness: 95.7% (of 8,784 expected hours; 2024 is a leap year)
- Source: https://www.ncei.noaa.gov/data/global-hourly/

NOAA data is public domain (U.S. government work).

## Results

**33 temperature anomalies detected** (|z| > 3.0)

- All 33 anomalies occur in April (n=21) and May (n=12) 2024
- Temperature range: 36.9–38.0°C
- Clustered 04:00–08:00 UTC (12pm–4pm local afternoon peaks)
- Consistent with documented extreme heat events in the Philippines (Sandford et al., 2025)

**Sensitivity:**

- |z| > 2.5: 122 anomalies (includes observations outside the heat wave period)
- |z| > 3.0: 33 anomalies (exclusively April–May)
- |z| > 3.5: 0 anomalies

See full results in published paper.

## Citation

If you use this code or data, please cite:

```
Thomas F. Heston MD. (2025). tomheston/blockchain-ai-climate-framework: Blockchain AI Study (v1.0.2). Zenodo. https://doi.org/10.5281/zenodo.17429218
```

## License

- **Code:** MIT License - Free to use, modify, distribute
- **Data:** Public domain (NOAA) / CC-BY-4.0 (derivatives)
- **Documentation:** CC-BY-4.0

## Reproducibility

All analysis is fully reproducible:

- Deterministic algorithm (global mean and standard deviation; no random components)
- Standard statistical methods (NumPy/Pandas)
- No proprietary software required
- Complete parameter documentation in paper

Expected runtime: < 1 minute

## Contact

**Thomas F. Heston, MD**  
University of Washington  
https://faculty.washington.edu/theston/contact  
ORCID: [0000-0002-5655-2512](https://orcid.org/0000-0002-5655-2512)

## Acknowledgments

NOAA National Centers for Environmental Information for providing open climate data.

---

**Repository archived on Zenodo:** https://doi.org/10.5281/zenodo.17429218  
**Last updated:** 2026-03-22
