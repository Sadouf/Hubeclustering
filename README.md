## Synthetic Commute Data Analysis

This repository contains a Python script for analyzing a synthetic commute diary dataset. The analysis includes data cleaning, feature engineering to compute CO₂ emissions based on commute modes, clustering of work locations to identify work hubs using DBSCAN, and optional visualization of the clustering results.

### Project Structure

```
├── README.md           # Project overview and instructions
├── requirements.txt    # Python dependencies
└── commute_analysis.py # Main analysis script
```

### Dataset

The analysis uses an Excel file named `RWHs_All_Users_Synthetic_Diary.xlsx`, containing the following relevant columns:

* `Distance to Work Location (km)` (numeric)
* `Commute Mode` (categorical: Car, Bus, Train, Walking, Biking)
* `Work Location Latitude` (numeric)
* `Work Location Longitude` (numeric)

Additional metadata columns are available but not required by the script.

### Dependencies

* Python 3.7+
* pandas
* numpy
* scikit-learn
* matplotlib

Install dependencies via:

```bash
pip install -r requirements.txt
```

### Usage

1. Place the dataset in the `input/` directory or update the file path in the script.
2. Run the analysis:

   ```bash
   python commute_analysis.py
   ```
3. The script will:

   * Load and clean the data (drop records with missing commute fields).
   * Compute a new column `CO2_emission` (kg per trip) based on predefined emission factors.
   * Perform DBSCAN clustering on work location coordinates to identify clusters (work hubs).
   * Print summary statistics and clustering results.
   * Optional: display a scatter plot of clusters.

### Feature Engineering

* **CO₂ Emissions**: Computed as `distance * emission_factor`, where emission factors (kg/km) are defined for each commute mode:

  * Car: 0.271
  * Bus: 0.089
  * Train: 0.041
  * Walking & Biking: 0

### Clustering

* Uses **DBSCAN** with parameters:

  * `eps=0.01` (approx. \~1km radius depending on coordinate scale)
  * `min_samples=5`
* Noise points are labeled `-1`.
* Outputs the number of clusters and noise points.

### Visualization

A scatter plot of longitude vs. latitude colored by cluster label is shown using `matplotlib`.

### Customization

* Adjust `eps` and `min_samples` in the DBSCAN initialization to tune clustering granularity.
* Modify emission factors or commute modes in `emission_factors` as needed.

### License

This project is released under the MIT License.
