---
layout: post
title: Machine Learning for Web Tracking and Detection
date: 2024-10-30
categories: [Project, AI]
tags: [project, privacy, application, cybersecurity, network, compliance-assessment, machine-learning, AI, web, data-security]
---

# Machine Learning for Web Tracking Detection and Classification

The objective of this task was to differentiate JavaScript code into functional or tracking categories by utilizing two machine learning models: One-Class SVM and Baseline SVM. These models were trained and tested on a dataset composed of labelled JavaScript code samples. The One-Class SVM, a single-class model, was trained to discern patterns in tracking JavaScript code, with the aim of classifying new code samples as either functional or anomalous. On the other hand, the Baseline SVM model served as a standard for comparison. The evaluation of these models provided valuable insights into their accuracy and efficiency in classifying JavaScript code. This report will outline the process of implementing these machine learning models on the JavaScript code dataset and summarize the results, illustrating the models' competencies in categorizing the code as either functional or tracking based on their performance indicators.


### Tools Used

- **Scikit-Learn (One-Class SVM and Baseline SVM)**: Machine learning models were used to classify JavaScript code as functional or tracking by analyzing patterns in the code.
- **TF-IDF (Term Frequency-Inverse Document Frequency)**: A feature extraction method applied to JavaScript code samples to convert textual data into numerical features, essential for model training.

### Skills Learned

- **Machine Learning for Security**: Gained experience in training One-Class SVM for anomaly detection and Baseline SVM for classification, specifically in distinguishing tracking from functional JavaScript.
- **Feature Engineering and Extraction**: Used TF-IDF to create features from JavaScript code, transforming raw code data into structured input suitable for machine learning models.
- **Model Evaluation and Tuning**: Enhanced understanding of model validation, testing, and parameter tuning techniques to improve accuracy, specifically adjusting parameters such as nu and gamma in One-Class SVM to balance model performance.
- **Web Tracking Analysis**: Developed a foundation in analyzing web tracking behavior by categorizing JavaScript based on functionality, an essential skill for privacy and security analysis within cybersecurity contexts.

## Steps

### DATA PREPROCESSING
There are two datasets containing JavaScript files categorized for tracking and functionality. The preprocessing of these files was accomplished as follows:

The files are located in two separate directories: LabelledData/functionalJS and LabelledData/trackingJS. They are accessed directly by providing their path addresses.
Using the provided code on iLearn, the content of each file was read using codecs to manage potential encoding issues and then stored in two lists: rusefulJSfiles and ruselessJSfiles.
Corresponding labels were created: [-1] for useful JavaScript files and [1] for useless JavaScript files.


### FEATURE EXTRACTION
Term Frequency-Inverse Document Frequency (TF-IDF) was employed to extract features from both functional and tracking JavaScript codes. In this process, JavaScript codes were transformed into features through TF-IDF vectorization. The vectorizer was initiated at 190 to maximize the number of features, then the fit_transform method was used to compute the TF-IDF features from the combined JavaScript code dataset. Additionally, the TF-IDF features from the tracking JavaScript code dataset were separately computed for model training.


### MODEL TRAINING, VALIDATION AND TESTING WITH PARAMETER TUNING
As a machine learning model based on a single class, the One-Class SVM was trained on trackingJS codes (ruselessJSfiles) only, and TF-IDF features for tracking JavaScript codes were computed along with normalization. Regarding the kernel, the Radial Basis Function (RBF) Kernel (default) was considered due to its compatibility for most cases where the data is not linearly separable. It can capture complex relationships between data points. Furthermore, the given code from iLearn provided gmv and nuv parameters as a suggestion for the RBF kernel, and therefore they are used for model training, validation, and testing phases. After that, the validation and test predictions of the One-class model were mapped back to the labels initially indicated to match the original labelling.

The Baseline SVM was trained using both functional and tracking JavaScript codes from the dataset, serving as a benchmark for performance comparison. Evaluation was carried out utilizing classification report data for each phase. Initially, the dataset was divided such that 80% was allocated for model training and 20% for testing. To identify potential overfitting or underfitting of the models, the dataset was later redistributed as follows: 60% for training, 20% for validation, 20% for testing.

To potentially improve the classification performance of the One-Class SVM model, variable values of parameters were experimented with to identify the best model for training and evaluation. Specifically, the ‘nu’ parameter ranged from 0.01 to 0.5 to experiment with levels of strictness for the boundary created by the One-class model, while the ‘gamma’ parameter was set to ‘auto’ to help prevent overfitting by reducing the influence of each feature and ‘scale’ to consider the distribution of data and normalize the effect of ‘gamma’ based on the spread of the features.

### RESULT AND DISCUSSION
After implemented directories for each type of JavaScript files, the number of files was shown as follow: 

![number of JS files](https://github.com/user-attachments/assets/cf71c11e-5921-4c8c-a3f5-fa6a94909a6b)
_Output of numbers of JS files from the dataset by Types._

After feature extraction and data normalization, the dataset was divided into training, validation, and testing subsets with the ratios indicated above. The One-Class SVM with the default RBF kernel (gamma = 0.001 and nu = 0.001) was trained on the Tracking JS (uselessJS), and predictions were made on the test set. These results were then compared to the outcomes from the Baseline SVM, which was trained on the entire dataset. The results presented a prediction accuracy of 56% for the One-Class SVM compared to 76% for the Baseline SVM.

![report on training of svm and baseline](https://github.com/user-attachments/assets/3f26e9b1-76b8-4a19-9bb7-bf511e8a7bc4)
_Classification Report on Training subset of One-Class SVM and Baseline SVM models._

Subsequently, the models' performances were assessed using validation and testing subsets to effectively demonstrate the progression and efficiency of the single-class model under development. The Validation and Testing Accuracy of the One-Class SVM were 56.32% and 56.02%, respectively, compared to the Baseline SVM, which achieved accuracies of 73.18% and 72.66%. The resulting outcomes are presented as follows:

![report on validation subset of svm and baseline](https://github.com/user-attachments/assets/a0b7fd8a-11d0-4ccb-b142-cf0886a406e9)
_Classification Report on Validation subset of One-Class SVM and Baseline SVM._

![report on testing of svm and baseline](https://github.com/user-attachments/assets/b079780c-9e7d-4786-824d-400f106552e1)
_Classification Report on Testing subset of One-Class SVM and Baseline SVM._


To enhance the classification performance, the One-Class SVM model underwent training and evaluation with parameter tuning to determine optimal values. The best parameters were identified as nu: 0.1 and gamma: scale, resulting in a validation accuracy of 60.34%. Subsequently, the model was tested using these optimal parameters and compared with the baseline SVM. The results indicated that the One-Class SVM's testing accuracy increased to 59%, a significant improvement over the default parameters (nu: 0.001 and gamma: 0.001). However, despite this improvement, the One-Class SVM's performance was still weak compared to the Baseline SVM, indicating a struggle to generalize as effectively as the Baseline SVM for this task.

### CONCLUSION
In conclusion, the machine learning models One-Class SVM and Baseline SVM were utilized to categorize JavaScript code into functional and tracking categories. The Baseline SVM, trained on both functional and tracking JavaScript code, significantly outperformed the One-Class SVM, which was trained solely on tracking JavaScript code. Even after parameter tuning, the One-Class SVM failed to match the performance of the Baseline SVM, indicating that the Baseline SVM is a more effective tool for this task. These findings could be highly beneficial for future practical applications in web tracking and JavaScript code categorization. Further improvements to the One-Class SVM model might show better performance in the future by exploring more advanced feature extraction methods or using larger and more balanced training datasets.