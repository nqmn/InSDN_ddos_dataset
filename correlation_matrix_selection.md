# Feature Correlation Analysis for SDN Dataset

This script performs a statistical correlation analysis on the dataset `insdn_ddos_binary_0n1d.csv`. It compares the strength of relationships between numerical features using three correlation methods: **Pearson**, **Spearman**, and **Kendall**.

### File & Scripts:
You can access the file here:
```
kendall_dataset_distributions.ipynb
```

### Dataset involved
- InSDN
- HLD-DDoSDN
- LR-HR DDoS 2024 Dataset for SDN-Based Networks

## Main Steps
1. Load and Prepare the Data
    - The dataset is read using pandas.
    - The Label column (if present) is dropped.
    - Only numerical columns are retained (non-numeric/categorical data is excluded).

2. Compute Correlation Matrices
    - Correlation is computed using three methods:
      - **Pearson** – linear correlation
      - **Spearman** – monotonic rank correlation
      - **Kendall** – ordinal association

3. Extract Upper Triangle Correlation Values
    - Only the upper triangle (excluding the diagonal) of each correlation matrix is extracted.
    - Absolute values are used to focus on the strength of relationships, regardless of direction.

4. Compute Summary Statistics
    - Mean and Standard Deviation are calculated for each correlation method to summarize the overall strength and consistency of relationships.

5. Interpret the Results
    - Based on the average correlation:
      - \> 0.5 → strong relationship
      - \> 0.3–0.5 → moderate relationship
      - \> < 0.3 → weak or negligible relationship

6. Recommendation of Correlation Method
    - The method with the highest mean and lowest standard deviation is considered most suitable for the dataset.
    - If different methods win in each category, a balanced method (typically Spearman) is recommended.

### Optional: Save Results
To save correlation matrices for further analysis or visualization:

```python
pearson_corr.to_csv("pearson_correlation.csv")
spearman_corr.to_csv("spearman_correlation.csv")
kendall_corr.to_csv("kendall_correlation.csv")
```

## Experiments on 3 Datasets

#### Result on `InSDN dataset`:
```
=== Statistik Korelasi ===
Purata Pearson:  0.1635 | Sisihan Piawai: 0.2440
Purata Spearman: 0.5368 | Sisihan Piawai: 0.2752
Purata Kendall:  0.4796 | Sisihan Piawai: 0.2533

=== Tafsiran ===
- Pearson r ≈ 0.16 ± 0.24: Hubungan lemah atau tidak ketara.
- Spearman ρ ≈ 0.54 ± 0.28: Hubungan kuat.
- Kendall τ ≈ 0.48 ± 0.25: Hubungan sederhana.

=== Cadangan Penggunaan Korelasi ===
- Corak bercampur; tiada satu metrik unggul mutlak.
- Purata tertinggi: **Spearman**; Sisihan piawai terendah: **Pearson**.
- Fokus pada Spearman untuk keseimbangan linear & monotonik.
```

#### Result on `HLD-DDoSDN`:

```

```

#### Result on `LR-HR DDoS 2024 Dataset for SDN-Based Networks`:

```
=== Statistik Korelasi ===
Purata Pearson:  0.1302 | Sisihan Piawai: 0.2016
Purata Spearman: 0.5481 | Sisihan Piawai: 0.3172
Purata Kendall:  0.4836 | Sisihan Piawai: 0.2802

=== Tafsiran ===
- Pearson r ≈ 0.13 ± 0.20: Hubungan lemah atau tidak ketara.
- Spearman ρ ≈ 0.55 ± 0.32: Hubungan kuat.
- Kendall τ ≈ 0.48 ± 0.28: Hubungan sederhana.

=== Cadangan Penggunaan Korelasi ===
- Corak bercampur; tiada satu metrik unggul mutlak.
- Purata tertinggi: **Spearman**; Sisihan piawai terendah: **Pearson**.
- Fokus pada Spearman untuk keseimbangan linear & monotonik.
```

## Performance analysis on datasets 

1. Model: DecisionTreeClassifier()
2. The metric involved is accuracy.

#### Output:

| Dataset    | Pearson   | Spearman  | Silhouette  | Winner |
|------------|-----------|-----------|-------------|--------|
| InSDN      | 0.999543  |           | 0.8999      |    /   |
|            |           | 0.999800  | 0.9271      |        |
| LR-HR      | 0.999868  |           | 0.9159      |    =   |
|            |           | 0.999868  | 0.9081      |    =   |
| HLD-DDoSDN | 1.0       |           | 0.2389      |    =   |
|            |           | 1.0       | 0.2389      |    =   |

### Analysis:

In all datasets, both Pearson and Spearman show extremely high correlation, meaning both methods agree that the features are strongly related.
However, in InSDN, **Spearman** is slightly higher than Pearson — this might suggest non-linear monotonic relationships in the data.
In HLD-DDoSDN and LR-HR, they are identical, meaning the relationships are both strong and linear.

### Recommendation

#### Correlation Analysis:

Based on the correlation results across the three datasets (InSDN, HLD-DDoSDN, and LR-HR), the **Spearman** method consistently yields correlation values that are:
    - Equal to or slightly higher than Pearson,
    - More robust to non-linear relationships,
    - And more tolerant of outliers and non-normal distributions.

Therefore, it is suggested that the **Spearman** method is better suited for evaluating feature relationships in these datasets.
This makes Spearman a safer and more general-purpose choice, especially in scenarios where the data structure or distribution is not guaranteed to be linear or normal.

#### Performance Analysis:

- On the `InSDN` dataset, *Spearman* achieved higher accuracy than Pearson, suggesting better performance for that case.
- On `HLD-DDoSDN` and `LR-HR`, both methods produced identical results.
- Given that Spearman is equal or better in all datasets:
    - It is recommended to use the *Spearman* method as it provides slightly better or equivalent accuracy across different datasets.

Additionally, *Spearman*'s ability to capture monotonic (not just linear) relationships gives it an advantage in more complex or non-linear feature spaces.
