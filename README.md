# Clustering Mini Project - Wholesale Customer Segmentation

This repository contains four individual clustering analyses completed by the team using the **Wholesale Customers Dataset**.

Each team member applied and compared:

- K-Means Clustering
- DBSCAN
- Hierarchical Clustering

Although everyone used the same dataset, each analysis selected different spending features, cluster numbers, and DBSCAN parameters. This allowed the team to observe how feature selection and parameter choices affect clustering results.

---

## Project Objective

The objective of this project is to:

1. Prepare and scale a real customer dataset.
2. Apply three clustering algorithms.
3. Visualize the resulting customer groups.
4. Evaluate the models using the Silhouette Score.
5. Compare cluster shapes, number of clusters, and noise sensitivity.
6. Identify the most suitable algorithm for each selected feature set.

---

## Dataset

The **Wholesale Customers Dataset** contains annual spending information for **440 customers**.

### Columns

| Column | Description |
|---|---|
| `Channel` | Customer channel category |
| `Region` | Customer region category |
| `Fresh` | Annual spending on fresh products |
| `Milk` | Annual spending on milk products |
| `Grocery` | Annual spending on grocery products |
| `Frozen` | Annual spending on frozen products |
| `Detergents_Paper` | Annual spending on detergents and paper products |
| `Delicassen` | Annual spending on delicatessen products |

The dataset contains no missing values. All team members applied `StandardScaler` before clustering because the algorithms rely on distances between observations.

---

## Team Members and Approaches

| Team Member | Notebook | Features Used | Main Difference |
|---|---|---|---|
| **Rana Aljuaid** | [`RanaAljuaidUnsupervisedP1.ipynb`](RanaAljuaidUnsupervisedP1.ipynb) | `Milk`, `Grocery` | Simple two-feature analysis with DBSCAN parameter testing |
| **Mohammed Alhejaili** | [`Mohammed_Alhejaili_ipynb.ipynb`](Mohammed_Alhejaili_ipynb.ipynb) | `Grocery_ratio`, `Detergents_ratio` | Created spending-ratio features instead of using raw spending |
| **Riyadh Ahmed** | [`Riyadh_ahmed_Clustering_Wholesale_Customers_FreshMilk.ipynb`](Riyadh_ahmed_Clustering_Wholesale_Customers_FreshMilk.ipynb) | `Fresh`, `Milk` | Used three clusters and a k-distance graph for DBSCAN |
| **Sumaya Hassan** | [`Sumaya_Hassan_U4_MiniProject.ipynb`](Sumaya_Hassan_U4_MiniProject.ipynb) | `Grocery`, `Detergents_Paper` | Explored different cluster and DBSCAN settings |

---

# Individual Results

## 1. Rana Aljuaid

### Selected Features

- Milk
- Grocery

### Preprocessing

- Checked missing values
- Selected two numerical features
- Applied `StandardScaler`
- Used direct 2D scatter plots without PCA

### Model Settings

| Algorithm | Settings |
|---|---|
| K-Means | `n_clusters=2` |
| DBSCAN | `eps=0.6`, `min_samples=5` |
| Hierarchical | `n_clusters=2`, Ward linkage |

Rana tested several combinations of `eps` and `min_samples` before choosing the final DBSCAN settings.

### Results

| Algorithm | Clusters | Noise Points | Silhouette Score |
|---|---:|---:|---:|
| K-Means | 2 | 0 | 0.706 |
| DBSCAN | 2 | 20 | 0.649 |
| Hierarchical | 2 | 0 | **0.746** |

### Conclusion

Hierarchical Clustering performed best for the selected Milk and Grocery features. K-Means also produced clear groups, while DBSCAN identified 20 unusual customers as noise.

---

## 2. Mohammed Alhejaili

### Selected Features

Mohammed first considered all six spending columns, then created two new ratio-based features:

- `Grocery_ratio`
- `Detergents_ratio`

The ratios represent each category as a proportion of a customer's total spending.

### Preprocessing

- Checked and explored all spending columns
- Created engineered ratio features
- Applied `StandardScaler`
- Used direct 2D visualization
- Used a k-distance graph to guide DBSCAN parameter selection

### Model Settings

| Algorithm | Settings |
|---|---|
| K-Means | `n_clusters=2` |
| DBSCAN | `eps=0.20`, `min_samples=5` |
| Hierarchical | `n_clusters=2`, Ward linkage |

### Results

| Algorithm | Clusters | Noise Points | Silhouette Score |
|---|---:|---:|---:|
| K-Means | 2 | 0 | **0.599** |
| DBSCAN | 2 | 71 | 0.473 |
| Hierarchical | 2 | 0 | 0.595 |

### Conclusion

K-Means achieved the highest score, closely followed by Hierarchical Clustering. The ratio features separated customers according to how much of their total spending went toward Grocery and Detergents/Paper products. DBSCAN detected the same general structure but classified 71 customers as noise.

---

## 3. Riyadh Ahmed

### Selected Features

- Fresh
- Milk

### Preprocessing

- Selected two raw spending variables
- Applied `StandardScaler`
- Used direct 2D visualization
- Used the Elbow Method for K-Means
- Used a k-distance graph for DBSCAN

### Model Settings

| Algorithm | Settings |
|---|---|
| K-Means | `n_clusters=3` |
| DBSCAN | `eps=0.3`, `min_samples=5` |
| Hierarchical | `n_clusters=3`, Ward linkage |

### Results

| Algorithm | Clusters | Noise Points | Silhouette Score |
|---|---:|---:|---:|
| K-Means | 3 | 0 | **0.533** |
| DBSCAN | 3 | 35 | 0.486 |
| Hierarchical | 3 | 0 | 0.458 |

### Conclusion

K-Means performed best for Fresh and Milk spending. DBSCAN was useful for identifying 35 unusual high-spending customers, while Hierarchical Clustering produced a similar but slightly less separated structure.

---

## 4. Sumaya Hassan

### Selected Features

- Grocery
- Detergents_Paper

### Preprocessing

- Checked data types, missing values, and duplicates
- Selected two numerical spending variables
- Applied `StandardScaler`
- Used direct 2D scatter plots

### Model Settings Explored

| Stage | Algorithm | Settings |
|---|---|---|
| Visualization | K-Means | `n_clusters=4` |
| Evaluation | K-Means | `n_clusters=6` |
| Final comparison | Hierarchical | `n_clusters=3` |
| Visualization | DBSCAN | `eps=0.5`, `min_samples=5` |
| Evaluation | DBSCAN | `eps=1.0`, `min_samples=6` |

### Evaluation Results

| Algorithm | Clusters Used | Noise Points | Silhouette Score |
|---|---:|---:|---:|
| K-Means | 6 | 0 | 0.593 |
| Hierarchical | 3 | 0 | **0.655** |
| DBSCAN | 1 non-noise cluster | 5 | Not defined |

DBSCAN's Silhouette Score was not defined because the evaluated settings produced only one non-noise cluster. A Silhouette Score requires at least two clusters.

### Conclusion

Hierarchical Clustering achieved the strongest valid Silhouette Score in Sumaya's evaluation. Her notebook also demonstrates how changing the number of clusters and DBSCAN parameters can produce different outcomes.

---

# Overall Comparison

## Best Result in Each Notebook

| Team Member | Best Algorithm | Best Silhouette Score |
|---|---|---:|
| Rana Aljuaid | Hierarchical | **0.746** |
| Mohammed Alhejaili | K-Means | **0.599** |
| Riyadh Ahmed | K-Means | **0.533** |
| Sumaya Hassan | Hierarchical | **0.655** |

> **Important:** The scores were calculated using different feature sets, so they should not be treated as a direct competition. A Silhouette Score is most useful for comparing models applied to the same feature space.

---

## Main Differences Between the Team Members

### 1. Feature Selection

Each member studied a different customer-spending relationship:

| Team Member | Feature Relationship |
|---|---|
| Rana | Milk spending compared with Grocery spending |
| Mohammed | Grocery and Detergents/Paper as proportions of total spending |
| Riyadh | Fresh spending compared with Milk spending |
| Sumaya | Grocery spending compared with Detergents/Paper spending |

Feature selection changes the distances between customers, so the same customer may belong to different clusters in different notebooks.

### 2. Number of Clusters

- Rana and Mohammed selected **two clusters**.
- Riyadh selected **three clusters**.
- Sumaya explored **three, four, and six clusters**, depending on the algorithm and experiment.
- DBSCAN discovered its own number of clusters based on density rather than receiving a fixed value.

### 3. DBSCAN Parameters and Noise

| Team Member | `eps` | `min_samples` | DBSCAN Clusters | Noise Points |
|---|---:|---:|---:|---:|
| Rana | 0.6 | 5 | 2 | 20 |
| Mohammed | 0.20 | 5 | 2 | 71 |
| Riyadh | 0.3 | 5 | 3 | 35 |
| Sumaya — evaluated setting | 1.0 | 6 | 1 | 5 |

The number of noise points differs because DBSCAN is highly sensitive to:

- The features used
- The scale and distribution of those features
- `eps`
- `min_samples`

A smaller `eps` usually creates more noise because each point must have nearby neighbors within a smaller distance.

### 4. Best-Performing Algorithm

- K-Means performed best in Mohammed's and Riyadh's analyses.
- Hierarchical Clustering performed best in Rana's and Sumaya's analyses.
- DBSCAN was not the highest-scoring model, but it was the only algorithm that explicitly identified noise and unusual customers.

---

# Key Team Insights

1. **Scaling was essential.**  
   All algorithms use distance, so StandardScaler prevented large-value variables from dominating the clusters.

2. **Feature selection strongly affected the result.**  
   Milk and Grocery produced a different structure from Fresh and Milk or ratio-based features.

3. **There is no single universal cluster count.**  
   The appropriate number depends on the selected features and the method used to evaluate the structure.

4. **K-Means was simple and effective.**  
   It performed best in two analyses and was easy to visualize and interpret.

5. **Hierarchical Clustering produced the highest individual score.**  
   Rana's Hierarchical model achieved a Silhouette Score of 0.746.

6. **DBSCAN was valuable for outlier detection.**  
   It classified unusual customers as noise instead of forcing every customer into a cluster.

7. **Silhouette Scores must be interpreted carefully.**  
   Scores from different feature sets are not fully comparable, and DBSCAN's score should be calculated only when at least two non-noise clusters exist.

---

# Algorithm Comparison

| Algorithm | Strengths | Limitations |
|---|---|---|
| K-Means | Fast, simple, interpretable, suitable for compact groups | Requires choosing K and assigns every point to a cluster |
| DBSCAN | Detects noise, does not require K, can find irregular shapes | Sensitive to `eps` and `min_samples`; may find only one cluster |
| Hierarchical | Provides a dendrogram and shows nested relationships | Can be slower and does not directly identify noise |

---

# Final Conclusion

The team successfully applied and compared three clustering algorithms to the same wholesale customer dataset using different feature combinations.

The results demonstrate that clustering is influenced not only by the chosen algorithm, but also by:

- Feature selection
- Feature engineering
- Scaling
- Number of clusters
- Density parameters

K-Means and Hierarchical Clustering were generally the most suitable methods for creating customer segments. DBSCAN added a different perspective by identifying customers with unusual spending behavior as noise.

---

# Repository Structure

```text
Clustering-Mini-Project/
│
├── README.md
├── Wholesale customers data.csv
├── RanaAljuaidUnsupervisedP1.ipynb
├── Mohammed_Alhejaili_ipynb.ipynb
├── Riyadh_ahmed_Clustering_Wholesale_Customers_FreshMilk.ipynb
└── Sumaya_Hassan_U4_MiniProject.ipynb
```

---

# How to Run the Project

1. Clone the repository:

```bash
git clone https://github.com/ranatsa9/Clustering-Mini-Project-.git
```

2. Open the project folder.

3. Install the required libraries:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter
```

4. Start Jupyter Notebook:

```bash
jupyter notebook
```

5. Open any team member's notebook and run the cells in order.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- SciPy
- Jupyter Notebook
