# Hosting Capacity Map

Data-driven Hosting Capacity Map for distribution networks.

This project provides an interactive Hosting Capacity Map (HCM) for visualizing transformer-level hosting capacity in the IEEE 123-bus distribution system.

The system combines feeder topology, transformer information, hosting-capacity results, and GIS-based visualization to support intuitive comparison and inspection of hosting-capacity results.

---

## Overview

The current HCM visualizes transformer-level Hosting Capacity (HC) on both:

- distribution network topology view
- GIS-based geographic map view

The current implementation is based on the IEEE 123-bus feeder and includes:

- 130 buses
- 126 distribution lines
- 95 service transformers
- transformer phase information
- transformer rating information
- Hosting Capacity color classification
- model-based and data-driven HC visualization
- transformer search
- phase filtering
- result-status filtering
- interactive transformer selection
- synthetic GIS placement on suburban roads in Pflugerville, Texas

---

## Supported Models

The HCM is designed to support the following Hosting Capacity results:

- Model-Based (QSTS Reference)
- Linear Regression (LR)
- Gradient Boosting Machine (GBM)
- LightGBM
- Long Short-Term Memory (LSTM)
- Graph Attention Network (GAT)
- LSTM-GAT
- GAT-PINN

The Model-Based result is currently used as the reference HC result.

The data-driven model results will be connected through individual transformer-phase HC result files when prediction results become available.

At the current development stage, if an individual model result file does not exist, the HCM uses temporary demonstration values derived from the Model-Based HC only for interface and visualization testing.

These temporary values are not research results.

---

## Hosting Capacity Workflow

The intended workflow of the system is:

1. Collect and preprocess distribution-system data
2. Predict voltage, active power, and reactive power using multiple data-driven models
3. Calculate Hosting Capacity for each model
4. Compare model-based and data-driven HC results
5. Combine voltage predictions using validation-error-based ensemble logic
6. Recalculate HC using the ensemble voltage prediction
7. Visualize transformer-level HC on the Hosting Capacity Map

The HCM does not directly average individual HC values.

When multiple models are selected, the intended ensemble process is:

Voltage prediction by multiple models  
→ validation-error-based voltage ensemble  
→ voltage constraint evaluation  
→ transformer thermal constraint evaluation  
→ Hosting Capacity calculation  
→ map visualization

---

## Hosting Capacity Rule

For quarterly Hosting Capacity results, the representative HC of each transformer is determined using:

```text
min(HC_Q2, HC_Q3, HC_Q4)
