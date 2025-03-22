
---

# Agentic Anomaly Detection System

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Version](https://img.shields.io/badge/version-1.0.0-blue)

An **Agentic System for Dynamic Anomaly Detection in Heterogeneous Data Using Gemini** – an automated, continuous pipeline that drastically reduces auditor workload (by up to 98%) by identifying and extracting data anomalies from worst-case quality datasets.

---

## Table of Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Pseudocode](#pseudocode)
- [Workload Reduction Analysis](#workload-reduction-analysis)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)
- [References](#references)

---
##  system architecutre: 

   ![WhatsApp Image 2025-03-22 at 17 48 23_f139e46d](https://github.com/user-attachments/assets/cca19df8-4bfb-4a05-a651-b3cf2e1dd7e8)
   

## Overview

This repository implements an agentic anomaly detection system that leverages the Gemini API to process and monitor heterogeneous datasets (e.g., restaurant data) in real time. The system consists of two main phases:

1. **Anomaly Type Identification:**  
   - Extracts column metadata from a raw CSV file.  
   - Generates a prompt using the metadata and queries the Gemini agent (e.g., *gemini-1.5-flash*) to identify potential anomaly types.  
   - Saves the resulting anomaly definitions in a JSON file.

2. **Anomaly Extraction and Binning:**  
   - Reanalyses the original CSV using the JSON anomaly definitions.  
   - Extracts rows exhibiting anomalies and bins them into new CSV files with unique names (using timestamps and counters).  
   - Operates continuously to monitor new data batches.

This design not only automates anomaly detection but also makes the system easily extendable to other domains where data quality is critical.

---

## System Architecture

The architecture is modular and divided into two distinct phases:

### Phase 1: Anomaly Type Identification
- **Input:** Raw CSV file  
- **Process:**  
  - Read and parse the CSV.  
  - Extract column metadata.  
  - Create a prompt for the Gemini agent to identify potential anomalies.  
  - Store the anomaly definitions as a JSON file.

### Phase 2: Anomaly Extraction and Binning
- **Input:** CSV file and JSON anomaly definitions  
- **Process:**  
  - Re-read the CSV file.
  - For each defined anomaly, extract the relevant columns.
  - Generate a prompt for the Gemini agent (e.g., *gemini-1.5-pro*).
  - Retrieve and save the anomaly rows to a new CSV file with proper timestamping and versioning.
- **Operation:** Designed for continuous and dynamic monitoring.

> **Figure 1:**  
> ![System Architecture](./diagram.png)  
> *Overview of the Agentic Anomaly Detection System*  
> *(Replace `diagram.png` with your actual architecture diagram.)*

---

## Features

- **Automated Anomaly Detection:**  
  Reduces manual intervention by up to 98% across multiple process stages.
  
- **Continuous Monitoring:**  
  Processes incoming data batches dynamically in a continuous loop.
  
- **Two-Phase Modular Pipeline:**  
  Separates anomaly type identification and extraction for improved maintainability.
  
- **Extensibility:**  
  Easily adaptable to various domains beyond the restaurant industry.
  
- **Versioning and Timestamping:**  
  Each output file is uniquely named to track changes over time.

---

## Installation

### Prerequisites

- Python 3.8 or higher
- Access to the Gemini API
- Required Python libraries (listed in `requirements.txt`)

### Steps

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/agentic-anomaly-detection.git
   cd agentic-anomaly-detection
   ```

2. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
   *(Ensure that the Gemini API libraries are installed and configured.)*

3. **Configuration:**
   - Update `config.json` with your CSV file path, Gemini API credentials, anomaly thresholds, etc.
   - Refer to `config.example.json` for guidance.

---

## Usage

### Running the System

To launch the anomaly detection process, execute:

```bash
python run_detection.py --input path/to/your/data.csv --config config.json
```

### Command-Line Arguments

- `--input`: Path to the CSV file containing the raw data.
- `--config`: Path to the configuration file with settings for the detection process.

### Output

- **JSON File:** Contains anomaly definitions from Phase 1.
- **CSV Files:** Generated for each detected anomaly batch, uniquely named with timestamps and version counters.

---

## Pseudocode

Below is a simplified representation of the core algorithms:

```pseudo
Algorithm 1: Anomaly Type Identification
1: Input: CSV file F
2: Read F into DataFrame D
3: Extract column names C from D
4: Generate prompt P1 with column metadata
5: Send P1 to Gemini Agent (gemini-1.5-flash)
6: Receive anomaly definitions A
7: Save A in JSON format for future use

Algorithm 2: Continuous Anomaly Extraction
1: Input: CSV file F and JSON anomaly definitions A
2: Read F into DataFrame D
3: For each anomaly a in A:
   a) Extract relevant columns Ca from D
   b) Generate prompt P2 using Ca
   c) Send P2 to Gemini Agent (gemini-1.5-pro)
   d) Receive anomaly rows Ra
   e) Append timestamp and version counter
   f) Save Ra as a CSV file
4: Repeat continuously for new data batches
```

---

## Workload Reduction Analysis

The system dramatically decreases the manual workload associated with data anomaly detection. Below is a comparison of workload distribution between manual and automated processes:

| Process Stage       | Manual (% Workload) | Automated (% Workload) |
|---------------------|---------------------|------------------------|
| Data Ingestion      | 30%                 | 2%                     |
| Preprocessing       | 25%                 | 1%                     |
| Anomaly Detection   | 35%                 | 2%                     |
| Insight Generation  | 10%                 | 1%                     |
| **Total**           | 100%                | 6%                     |

*Figure 2* (referenced in the paper) visually illustrates this dramatic reduction.

---

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create your feature branch:
   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. Commit your changes:
   ```bash
   git commit -m 'Add some AmazingFeature'
   ```
4. Push to your branch:
   ```bash
   git push origin feature/AmazingFeature
   ```
5. Open a Pull Request.

---

## License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---

## Acknowledgements

We thank the research team and domain experts whose insights have been invaluable in the development of this system. Special thanks also to the contributors and maintainers who continuously improve this project.

---

## References

- **Agentic System for Dynamic Anomaly Detection in Heterogeneous Data Using Gemini**  
  *(Refer to `research.pdf` in this repository for the complete paper.)*

---

*For any questions or further support, please open an issue or contact the project maintainers.*

---
