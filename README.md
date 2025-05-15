# InSDN Dataset Preparation for Binary Classification

This repository contains code and instructions for preprocessing the **InSDN Dataset** to support binary classification tasks in the context of DDoS detection in Software-Defined Networking (SDN) environments.

## 📌 Project Purpose

The notebook `insdn_preparation_binary.ipynb` is designed to:
- Load and merge multiple CSV files from the InSDN dataset directory.
- Clean and prepare the data for binary classification.
- Encode labels and features.
- Split the dataset into training and testing sets.
- Export the preprocessed datasets for downstream machine learning tasks.

This is particularly useful for researchers and practitioners building lightweight and adaptive ML models for SDN security systems.

## Project Structure
- [insdn_preparation_binary.ipynb](insdn_preparation_binary.ipynb)
- [correlation_analysis_sdn_datasets.ipynb](correlation_analysis_sdn_datasets.ipynb) ([README.md](correlation_method_selection.md))

---

## 📊 Dataset Information

- Each CSV file contains **84 features** extracted from SDN traffic.
- Files include both **benign** and **malicious** samples (e.g., from metasploitable-2).
- Final merged dataset has ~344,000 records.

---

## 🔧 Preprocessing Steps

1. **Data Loading**
   - Read and concatenate all CSV files in the dataset directory using `pandas`.

2. **Initial Inspection**
   - Set pandas display options to show all rows/columns for inspection.

3. **Label Encoding**
   - Convert categorical labels into binary format (e.g., `Normal` = 0, `Attack` = 1).

4. **Feature Cleaning**
   - Remove irrelevant or redundant features (e.g., timestamps, flow IDs, etc.).

5. **Train-Test Split**
   - Stratified split (e.g., 80/20) for balanced distribution of both classes.

6. **Exporting**
   - Save cleaned training and testing sets as CSV files for model ingestion.

---

## 🧪 Requirements

```bash
pip install pandas scikit-learn numpy
````

---

## 🚀 How to Use

1. Clone this repository:

   ```bash
   git clone https://github.com/your-username/insdn-binary-preparation.git
   cd insdn-binary-preparation
   ```

2. Add the dataset CSV files to the `1 dataset/` folder.

3. Open and run the notebook:

   ```bash
   jupyter notebook insdn_preparation_binary.ipynb
   ```

4. Preprocessed files will be saved in the working directory.

---

## 🔐 Use Case: SDN DDoS Detection

This preparation is a foundational step for:

* Lightweight machine learning models.
* Real-time DDoS detection in resource-constrained SDN environments.
* Adaptive and feature-aware classification pipelines.

---

## 🧠 Future Enhancements

* Add support for multiclass labeling.
* Integrate dynamic feature selection modules.
* Enable real-time preprocessing for streaming SDN data.

---

## 📜 License

This project is open-source and available under the [MIT License](LICENSE).

---

## 🤝 Acknowledgements

* [CIC InSDN Dataset](https://www.unb.ca/cic/datasets/insdn.html)
* SDN and ML research community for continuous contributions to cyber defense.

```
