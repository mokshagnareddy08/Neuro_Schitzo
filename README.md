Multi-Modal Independent Deep Learning Framework for Schizophrenia Detection
A deep-learning framework for schizophrenia detection using two complementary neuroimaging modalities: EEG and structural MRI. The project develops independent models for functional brain activity and structural brain abnormalities, without artificially pairing subjects across datasets.
Problem Statement
Schizophrenia is a complex psychiatric disorder that can be difficult to identify accurately using conventional clinical assessment alone. Neuroimaging modalities such as Electroencephalography (EEG) and Magnetic Resonance Imaging (MRI) provide complementary information about the brain:
- EEG captures functional/electrical brain activity over time.
- Structural MRI captures anatomical characteristics of the brain.
Existing approaches often focus on a single modality or require subject-matched multimodal datasets for feature fusion. In our case, the available EEG and MRI datasets contain different, non-overlapping subjects, making direct multimodal fusion scientifically inappropriate.
Therefore, the project aims to develop an approach that can exploit both modalities independently without artificial subject pairing.
Objective
The main objectives of this project are:
- Develop a deep-learning model for schizophrenia detection from EEG.
- Develop a separate deep-learning model for schizophrenia detection from structural MRI.
- Improve EEG representation learning using a CNN + Transformer architecture.
- Extract 3D anatomical features from MRI using 3D ResNet-18.
- Perform preprocessing and normalization appropriate for each modality.
- Evaluate both models using standard classification metrics.
- Compare the effectiveness of functional EEG and structural MRI for schizophrenia detection.
- Avoid unreliable multimodal fusion caused by unmatched subjects.
Proposed Solution
The proposed framework consists of two independently trained pipelines.
EEG Pipeline
Raw Multi-channel EEG
        ↓
Artifact Removal / ICA
        ↓
Band-pass Filtering
        ↓
Epoching
        ↓
Normalization
        ↓
1D CNN
        ↓
Patch / Token Embedding
        ↓
Positional Encoding
        ↓
Transformer Encoder
        ↓
Global Average / Attention Pooling
        ↓
EEG Embedding
        ↓
MLP Classifier
        ↓
Schizophrenia / Control

The 1D CNN extracts local temporal patterns from EEG signals, while the Transformer Encoder models relationships between different temporal regions of the signal. Global pooling converts the Transformer representation into a fixed-length EEG embedding for classification.
MRI Pipeline
T1-weighted MRI
        ↓
DICOM → NIfTI
        ↓
Orientation Correction
        ↓
Resampling
        ↓
Intensity Normalization
        ↓
Brain Extraction / Cropping
        ↓
3D ResNet-18
        ↓
Global Average Pooling
        ↓
MRI Embedding
        ↓
MLP Classifier
        ↓
Schizophrenia / Control

The 3D ResNet-18 learns spatial and anatomical features directly from the 3D structural MRI volume.
Why No Fusion?
The EEG and MRI datasets are not subject-matched. Therefore, an EEG record from one person cannot be artificially paired with an MRI scan from another person.
Instead:
EEG Dataset → EEG Model → Independent Prediction

MRI Dataset → MRI Model → Independent Prediction

This avoids introducing artificial subject relationships and potential data bias.
Datasets
EEG Dataset
The EEG dataset contains recordings from 81 subjects.
Important files include:
demographic.csv
columnLabels.csv
time.csv
mergedTrialData.csv
ERPdata.csv
1.csv
2.csv
...
81.csv

The numbered subject files contain the multichannel EEG measurements, while the other files provide demographic, channel, timing and ERP-related information.
The EEG pipeline uses the raw multichannel recordings as the primary model input.
Structural MRI Dataset
The MRI branch uses the COBRE (Collaborative Informatics and Neuroimaging Suite) structural MRI data, particularly T1-weighted anatomical MRI.
The MRI data is initially available in DICOM format and is converted into 3D NIfTI volumes before preprocessing and model training.
Dataset Relationship
The two datasets contain different subjects, so they are used independently rather than being fused at the feature or subject level.
Model Architecture
Modality	Input	Feature Extraction	Classifier
EEG	Multichannel EEG	1D CNN + Transformer	MLP
MRI	T1-weighted 3D MRI	3D ResNet-18	MLP


The framework therefore follows an independent multimodal learning strategy rather than conventional multimodal feature fusion.
Evaluation
Both models will be evaluated using standard binary-classification metrics:
- Accuracy
- Precision
- F1-score
- Sensitivity / Recall
- Specificity
- ROC-AUC
- Confusion Matrix
No performance values are reported here until the models have been trained and evaluated on the appropriate held-out subjects.
Results
Results will be updated after model training and subject-wise evaluation.

The final results section will report the performance of:
EEG Model
CNN + Transformer
Metric	Result
Accuracy	TBD
Precision	TBD
F1-score	TBD
Sensitivity	TBD
Specificity	TBD
ROC-AUC	TBD


MRI Model
3D ResNet-18
Metric	Result
Accuracy	TBD
Precision	TBD
F1-score	TBD
Sensitivity	TBD
Specificity	TBD
ROC-AUC	TBD


The results will also be compared to the base paper's approach to assess whether the proposed CNN-Transformer EEG architecture provides improved or complementary performance.
Key Contributions
- CNN + Transformer architecture for EEG-based schizophrenia detection.
- 3D ResNet-18 for structural MRI-based detection.
- Independent learning from functional and structural brain modalities.
- No artificial EEG–MRI subject pairing.
- Subject-wise evaluation to reduce data leakage.
- Comparison of functional EEG and structural MRI representations.
- Explainable and modular architecture allowing each modality to be evaluated independently.
Technology Stack
- Python
- PyTorch
- MNE
- NumPy
- Pandas
- SciPy
- Scikit-learn
- NiBabel
- 3D ResNet-18
- CNN
- Transformer Encoder
- DICOM / NIfTI
Project Status
🚧 Under Development
Current focus:
Dataset Preparation
        ↓
EEG Preprocessing
        ↓
CNN + Transformer
        ↓
MRI Preprocessing
        ↓
3D ResNet-18
        ↓
Training & Validation
        ↓
Performance Evaluation
        ↓
Final Comparison
