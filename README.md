# Phishing URL Detection
## Dataset Selection
The primary dataset used in this project is the Phishing Websites Dataset from the UCI Machine Learning Repository. This dataset contains 11,055 labeled website instances and 30 engineered numerical features that describe structural and behavioral characteristics associated with phishing activity. Each instance is labeled as either phishing or legitimate.
The dataset includes three major categories of features:
- URL and structural indicators, such as the presence of an IP address in the URL, URL length, prefix–suffix usage, and abnormal domain structures
- Domain and security signals, including SSL state, domain registration length, DNS records, and Google indexing
- Behavioral and interaction-based features, such as redirects, abnormal request patterns, anchor links, and pop-up behavior
These features were designed to capture common characteristics observed in phishing attacks, including domain manipulation, insecure communication channels, and deceptive interaction patterns.
Some limitations of this dataset include:
- The features are pre-engineered, which reduces flexibility in extracting additional raw lexical or semantic information from URLs
- The dataset was originally collected in 2012, so it may not fully reflect recent phishing strategies or domain obfuscation techniques
- The class distribution is moderately imbalanced (approximately 56% legitimate and 44% phishing), which may influence classifier performance
To address these limitations, we will incorporate robustness and generalization experiments, including testing performance stability under distribution shifts and evaluating threshold-based detection performance. If time permits, we may also incorporate an additional, more recent phishing dataset to strengthen generalization.
 
## Data Type Characterization
The dataset consists of structured tabular data in which each row represents a single website instance and each column corresponds to a numerical feature describing URL, domain, or behavioral characteristics.
All features are encoded as integer values, and the dataset contains no missing values. Most variables represent categorical or ordinal indicators encoded numerically (e.g., −1, 0, 1), reflecting suspicious, neutral, or legitimate behavior.
The dataset is labeled and supervised, with each instance classified as phishing or legitimate. It is also time-independent, meaning that samples are treated as independent observations with no temporal or sequential relationships. This simplifies modeling and allows the use of standard classification techniques.
 
## Data Science / Machine Learning Problem Definition
This project is formulated as a binary classification problem, where the goal is to classify a website as phishing or legitimate based on its engineered features.
The input feature matrix (X) consists of structured indicators capturing URL structure, domain registration, SSL usage, traffic signals, and abnormal behavioral patterns. The output variable (y) is a binary label indicating phishing or legitimate websites.
The original dataset uses labels of −1 (phishing) and 1 (legitimate). For consistency and reproducibility, we remap these labels to:
- Phishing = 1
- Legitimate = 0
This mapping is used consistently across all experiments and models.
Success in this project is defined as achieving high recall for phishing detection while maintaining a low false-positive rate. In security-sensitive systems, missing phishing URLs can lead to significant user risk, while excessive false positives reduce usability and trust. Therefore, the model should generalize well to previously unseen phishing domains and outperform simple rule-based or blacklist approaches.
 
## Why Data Science / Machine Learning?
A data-driven approach is well suited to phishing detection because phishing attacks evolve rapidly and often bypass static rule-based or blacklist systems. Blacklists are reactive and only block domains that have already been identified as malicious, making them ineffective against zero-day attacks.
Machine learning models can learn nonlinear interactions between structural and behavioral features and detect subtle patterns that may not be obvious to human analysts. These models can generalize to new, previously unseen phishing strategies and scale efficiently to large volumes of URLs, enabling real-time automated filtering. Additionally, machine learning reduces reliance on manual rule engineering and improves adaptability to evolving attacker behavior.
 
## Planned Approaches
### (a) Preprocessing and Feature Engineering
Because the dataset is structured and clean, preprocessing focuses on improving model stability and interpretability rather than raw feature extraction.
- Consistent label remapping and validation
- Train–test splitting with stratified sampling to preserve class proportions
- Feature scaling and normalization for models sensitive to feature magnitude (e.g., logistic regression and SVM)
- Handling moderate class imbalance through class weighting and comparative evaluation
- Exploratory data analysis to identify dominant predictive features
- Dimensionality reduction (e.g., PCA) if required to reduce redundancy or improve computational efficiency
- Feature importance and interpretability analysis using linear model coefficients and tree-based importance scores
- Model calibration and threshold tuning to optimize operational performance
 
### (b) Learning Methods and Models
We will compare several model types for both predictive performance and interpretability.

**Supervised Models**
- Logistic Regression (baseline)
- Decision Trees
- Random Forest and Gradient Boosting (primary tree-based models)
- Support Vector Machines

**Unsupervised and Anomaly Detection Models**
- k-Means clustering
- Gaussian Mixture Models

For the unsupervised approaches, clustering outputs will be converted into anomaly detection scores:
• For k-Means: distance from cluster centroids
• For GMM: negative log-likelihood under the learned probability distribution
A detection threshold will be selected using validation data to achieve a specified false-positive rate. This allows fair comparison between supervised and unsupervised approaches under equivalent operational constraints.
This model list may evolve based on exploratory analysis and performance results.
 
## Evaluation Plan
Our primary evaluation metric will be the F1-score, which balances precision and recall. However, phishing detection is a security-critical task, so we will also evaluate operational performance.
We will report:
- Precision, Recall, and F1-score
- Confusion matrices
- Recall at a fixed low false-positive rate
- Precision at high recall
- ROC and Precision–Recall curves
Operating thresholds will be selected using cross-validation or validation data only, ensuring unbiased test results.
We will use:
- An 80/20 train–test split
- 5-fold cross-validation for model selection and threshold tuning
Because the dataset is older, we will also evaluate robustness and generalization by testing model performance under distribution shift. This may include:
- Holding out subsets of URLs with different structural characteristics
- Evaluating performance sensitivity to threshold selection
- If feasible, testing on a newer phishing dataset
This approach will strengthen claims about real-world reliability and deployment readiness.      
