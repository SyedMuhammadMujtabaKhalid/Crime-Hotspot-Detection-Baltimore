# Crime Hotspot Detection - Baltimore

![License](https://img.shields.io/badge/License-MIT-blue.svg)
![Platform](https://img.shields.io/badge/Platform-KNIME-yellow)
![Algorithm](https://img.shields.io/badge/Algorithm-Random%20Forest-green)
![Dataset](https://img.shields.io/badge/Dataset-Baltimore%20Crime-orange)

## Project Overview

This repository contains the complete workflow and documentation for predicting and analyzing crime hotspots in Baltimore, Maryland. Using a robust dataset of 276,529 crime incidents spanning from 2012 to 2017, the project employs machine learning and spatial analysis techniques to classify and visualize high-risk crime areas. The primary tool utilized for this pipeline is the KNIME Analytics Platform.

## Problem Statement

Urban areas like Baltimore face significant challenges in allocating law enforcement resources effectively. Identifying patterns in criminal activity over time and space is critical for proactive policing. This project aims to accurately predict crime hotspots—regions with an exceptionally high density of criminal incidents—to assist in strategic resource deployment and public safety planning.

## Key Features

- **Spatial Aggregation:** Processing of spatial coordinate data (EPSG:4326) to define precise geographic regions.
- **Hotspot Classification:** Definition of "hotspots" using the 80th percentile threshold of crime occurrences.
- **Machine Learning Predictive Modeling:** Utilizing a Random Forest Classifier for accurate hotspot prediction.
- **Visual Analytics:** Generation of Kernel Density Estimation (KDE) Heatmaps to visualize the predicted hotspots.
- **Visual Programming Workflow:** Entire pipeline developed within the KNIME Analytics Platform for reproducibility and transparency.

## Dataset Information

The analysis is based on the **Baltimore Crime Dataset**, which includes:
- **Total Records:** 276,529 crime incidents.
- **Date Range:** 2012–2017.
- **Features:** Geospatial coordinates (latitude/longitude), timestamps, crime type, location descriptors, and weapon information.
- **Coordinate System:** EPSG:4326.

## Methodology

### Workflow Architecture
The core architecture follows a standardized Data Science pipeline: Data Ingestion -> Preprocessing -> Feature Engineering -> Modeling -> Evaluation -> Visualization. For a detailed breakdown, please refer to the [System Architecture Document](docs/architecture.md).

### Data Preprocessing
- **Missing Value Handling:** Removal or imputation of incomplete records, particularly missing spatial coordinates.
- **Temporal Parsing:** Extraction of day, month, year, and hour from the timestamp data.
- **Spatial Formatting:** Ensuring all latitude and longitude data conform to the EPSG:4326 standard.

### Feature Engineering
- **Spatial Aggregation:** Data is binned into defined geographical grids to calculate the frequency of crimes per area.
- **Temporal Features:** Aggregation based on time of day and seasonality.
- **Categorical Encoding:** Transformation of crime types and location descriptions into numerical formats suitable for machine learning.

### Hotspot Definition Strategy
A grid or region is classified as a "Hotspot" if its total crime frequency exceeds the **80th percentile** of the overall distribution across all regions. This rigorous threshold ensures that only the most critical areas are flagged.

### Machine Learning Model (Random Forest)
A **Random Forest Classifier** was chosen due to its robustness against overfitting and its ability to handle complex, non-linear relationships in spatial data.
- **Target Variable:** Binary classification (1 = Hotspot, 0 = Non-Hotspot).
- **Features Used:** Temporal, categorical, and spatially aggregated attributes.

### Spatial Analysis Approach & KDE Heatmap Generation
Using the predicted probabilities from the model, a **Kernel Density Estimation (KDE)** analysis is performed to create smooth, continuous heatmaps. This visual representation highlights the intensity of predicted crime occurrences across the city layout.

## Results & Performance

The model successfully identifies high-risk zones, allowing for the overlay of predicted hotspots on the map of Baltimore. The evaluation metrics (Accuracy, Precision, Recall, and F1-Score) from the KNIME workflow demonstrate a strong capability in discerning hotspot regions.

## Project Structure Tree

```
Crime-Hotspot-Detection-Baltimore/
├── .gitignore
├── CHANGELOG.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── Crime Hotspot Detection.pdf       # Original project report
├── Hotspot_Prediction.knwf           # Main KNIME workflow
└── docs/
    ├── architecture.md               # Detailed system architecture
    └── methodology.md                # In-depth methodology
```

## Installation Instructions

1. **Install KNIME:** Download and install the [KNIME Analytics Platform](https://www.knime.com/knime-analytics-platform).
2. **Clone the Repository:**
   ```bash
   git clone https://github.com/SyedMuhammadMujtabaKhalid/Crime-Hotspot-Detection-Baltimore.git
   cd Crime-Hotspot-Detection-Baltimore
   ```

## Usage Instructions

### KNIME Workflow Execution Guide
1. Open the KNIME Analytics Platform.
2. Select `File` > `Import KNIME Workflow...`
3. Choose `Select file` and browse to the cloned repository to select `Hotspot_Prediction.knwf`.
4. Click `Finish`.
5. Once imported, double-click the workflow in the KNIME Explorer to open it.
6. Click the `Execute All Executable Nodes` button (green double-play icon) in the toolbar.

### Dataset Preparation Guide
The workflow expects the Baltimore crime dataset. Please ensure the dataset file path in the 'CSV Reader' node matches your local directory or that the data is packaged within the workflow data area.

### Output Examples
Upon successful execution, the final nodes will display:
- Model performance metrics (Confusion Matrix, ROC Curve).
- A geographical KDE heatmap visualizing the hotspots.

## Future Improvements

- **Deep Learning Integration:** Implement Spatial-Temporal Graph Convolutional Networks (ST-GCN).
- **Real-Time Data Feed:** Connect the pipeline to a live API for dynamic daily hotspot prediction.
- **Socio-Economic Feature Addition:** Incorporate census data for deeper causative insights.

## Ethical Considerations

Predictive policing models run the risk of reinforcing existing biases in historical crime data. This project is intended for academic and research purposes to explore spatial data methodologies, not for deployment in active law enforcement without rigorous bias auditing and community oversight.

## References

- KNIME Analytics Platform Documentation
- OpenBaltimore Data Portal (Source of original dataset)

## Authors & Contributors

- **Syed Muhammad Mujtaba Khalid** - *Main Author*

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- University professors and research mentors.
- The open-source data science community.
