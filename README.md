# clustering-dry-beans
This project uses K-Means clustering to group seven types of dry beans based on their physical characteristics. The dataset includes 16 features derived from the shape and appearance of the beans. The goal is to create clusters that correspond to the known bean types and evaluate the effectiveness of the model in correctly identifying these types.

## Data

Link to dataset: https://archive.ics.uci.edu/dataset/602/dry+bean+dataset

### Features

The dataset includes the following features:

- **Area**
- **Perimeter**
- **MajorAxisLength**
- **MinorAxisLength**
- **AspectRatio**
- **Eccentricity**
- **ConvexArea**
- **EquivDiameter**
- **Solidity**
- **Extent**
- **Roundness**
- **Compactness**
- **ShapeFactor1**
- **ShapeFactor2**
- **ShapeFactor3**
- **ShapeFactor4**

### Bean Types

The dataset includes the following bean types:

- SEKER
- BARBUNYA
- BOMBAY
- CALI
- HOROZ
- SIRA
- DERMASON

## Methods

### Data Preprocessing

- **Feature Selection**: Initially, the model was fit using a subset of features—Perimeter, AspectRatio, and Eccentricity—before gradually incorporating more features to improve clustering results. A function was defined to efficiently fit and view the results of different feature combinations.
- **Normalization**: Features were standardized to ensure consistent scaling, which is crucial for effective clustering.

### Clustering

- **K-Means Clustering**: The K-Means algorithm was employed to cluster the beans into 7 groups. The model was initialized using the k-means++ method to improve convergence. Initially, three features were used, with additional features added later to refine the clusters.
- **Cluster Mapping**: After clustering, the majority class within each cluster was identified and mapped to the corresponding bean type. This provided a summary of the clustering results and allowed accurate conversion of the target column into an integer so that it can be compared with the model’s predictions.

### Model Evaluation

- **Homogeneity, Completeness, and V-Measure Scores**: These metrics were used to evaluate how well the clusters align with the true bean types. Improvements in these scores indicated better clustering alignment with the true labels.
- **Adjusted Rand Index (ARI)**: This index measures the similarity between the predicted clusters and the true labels, adjusted for chance.
- **Silhouette Score**: This score indicates how distinct or well-separated the clusters are, with higher scores indicating better separation.
- **Davies-Bouldin Index**: This index evaluates the average similarity ratio of each cluster with respect to the others, with lower values indicating better clustering.

## Results

- **Challenges**: The model struggled with distinguishing between certain bean types, particularly Cali and Barbunya beans, which often ended up in the same cluster despite efforts to separate them by introducing additional features like Roundness.
- **Key Findings**:
    - Initial clustering attempts resulted in multiple clusters being dominated by the same bean type, suggesting issues with homogeneity. It was also identified that an imbalance in the data as well as the similarities between bean types contributed to this issue.
    - By refining the feature set, the subsequent clustering achieved a better distribution, where each cluster had a different majority bean type.
    - To further refine the feature selection process and improve the evaluation metrics, Principal Component Analysis (PCA) was performed to reduce the dimensionality of the dataset and retain the few features with the most variance and therefore the most valuable information for the model.
    - Upon applying PCA, the issue of two clusters with the same majority class was reintroduced. This led to reducing the number of clusters to six so that two very similar beans would be grouped into the same cluster. This was due to the tradeoff between the overall accuracy of the model and the ability to differentiate between the two bean types.
    - After reducing the number of clusters, the model showed improvements in homogeneity, completeness, and V-Measure scores, indicating better alignment with true bean types. However, the Silhouette Score and Davies-Bouldin Index suggested that while clusters were more accurate, they were less distinct or compact compared to earlier iterations.

## Conclusion

This project demonstrates the application of K-Means clustering for categorizing dry beans based on physical characteristics. The final model showed significant improvements in clustering accuracy and alignment with true bean types. However, challenges remain in distinguishing between beans with similar shapes, suggesting that further refinement or alternative clustering methods may be needed for better performance.
