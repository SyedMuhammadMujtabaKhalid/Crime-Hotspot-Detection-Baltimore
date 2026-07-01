# Methodology

This document details the scientific approach and algorithms used in the Crime Hotspot Detection project.

## Hotspot Detection Flow

The core methodology is based on converting discrete crime points into continuous density maps and classifying specific regions based on statistical thresholds.

```mermaid
graph TD
    A[Raw Crime Coordinates] --> B[Spatial Aggregation]
    B --> C[Calculate Frequency per Region]
    C --> D{Is Frequency > 80th Percentile?}
    D -- Yes --> E[Classify as Hotspot (1)]
    D -- No --> F[Classify as Non-Hotspot (0)]
    E --> G[Machine Learning Training]
    F --> G
```

## 1. Spatial Aggregation (EPSG:4326)
All data points are processed using the EPSG:4326 coordinate reference system (WGS 84). The continuous coordinates (Latitude, Longitude) are mapped to discrete regions or grid cells across Baltimore.

## 2. Hotspot Definition Strategy
Rather than using arbitrary thresholds, a statistical approach is used:
*   The frequency of crime in every grid cell is calculated.
*   The 80th percentile of this frequency distribution is identified.
*   Any region with a crime frequency higher than the 80th percentile is labeled as a **Hotspot**.
*   This approach dynamically adjusts to the dataset's distribution, ensuring that only statistically significant high-crime areas are targeted.

## 3. Predictive Modeling (Random Forest)
A **Random Forest Classifier** is employed for its ability to handle high-dimensional spaces and non-linear relationships without excessive hyperparameter tuning.
*   **Ensemble Learning:** It builds multiple decision trees during training and outputs the mode of the classes for classification.
*   **Feature Importance:** It helps identify which features (e.g., time of day, location type) are most indicative of a hotspot.

## 4. Kernel Density Estimation (KDE)
To visualize the predicted hotspots, KDE is used.
*   Instead of plotting individual prediction points, KDE calculates the density of points within a given radius.
*   This creates a smooth, continuous heatmap surface.
*   Areas with high probability predictions merge to show intense "hot zones" on the visual map.

## Validation Strategy
The model's effectiveness is rigorously tested using a standard Train/Test split. Metrics extracted include:
*   **Confusion Matrix:** To track True Positives (correctly identified hotspots) vs. False Positives.
*   **ROC Curve / AUC:** To measure the model's ability to distinguish between the hotspot and non-hotspot classes across various thresholds.
