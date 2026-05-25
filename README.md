# Human Pose-Driven Fight Detection Using Random Forest and LSTM Architectures

## 📌 Project Description
This project focuses on developing an automated, lightweight violence detection system for real-time video surveillance. Instead of analyzing heavy, raw pixel data which often leads to high false-positive rates, this approach extracts 132 spatial coordinates representing human skeletal keypoints (66 body joints per frame) to model structural and physical interactions. 

To classify actions into "fight" or "no fight" categories, the project implements and evaluates three distinct models:
* **Long Short-Term Memory (LSTM):** Captures temporal relationships across consecutive frames, delivering the highest overall accuracy of **75%**.
* **Bidirectional Long Short-Term Memory (Bi-LSTM):** Analyzes sequence patterns in both forward and backward directions, yielding a moderate accuracy of **65%** due to dataset constraints.
* **Random Forest Classifier:** Used as a traditional, computationally light machine learning baseline, achieving an accuracy of **63%** but failing to capture sequence changes over time.

Ultimately, this project demonstrates that utilizing sequential deep learning models to track human pose dynamics provides an efficient, low-resource solution for automated security monitoring without requiring high-end computing setups.


## 🤖 Model Architectures & Descriptions

This project implements and compares three different types of machine learning and deep learning models to evaluate their effectiveness in capturing human pose dynamics for violence detection. 

### 1. Long Short-Term Memory (LSTM) Network
Long Short-Term Memory networks are a specialized type of Recurrent Neural Network (RNN) designed to learn long-term temporal dependencies in sequential data. This makes them ideal for video analysis, where the order and progression of frames matter.

* **Layer Configuration:** * **Input Layer:** Accepts sequence data with a standardized shape of `(30, 132)`, representing 30 consecutive video frames and 132 extracted coordinate features per frame.
  * **LSTM Layer:** Consists of 1 x 64 LSTM units to process and capture temporal tracking of the physical interactions over time.
  * **Regularization:** A Dropout layer set to `0.5` is placed right after the LSTM layer to prevent overfitting by randomly dropping node connections during training.
  * **Dense Hidden Layer:** A fully connected layer with 32 neurons using the **ReLU** (Rectified Linear Unit) activation function for feature mapping.
  * **Output Layer:** A final dense layer with 1 neuron utilizing a **Sigmoid** activation function to output a binary classification probability (Fight vs. No Fight).
* **Training Details:** Compiled using the **Adam optimizer** and **Binary Cross-Entropy loss** function, trained for 30 epochs with a batch size of 16.
* **Performance:** Achieved the highest testing accuracy of **75%**, demonstrating that tracking temporal patterns across frames is crucial for fight detection.

---

### 2. Bidirectional LSTM (Bi-LSTM) Network
The Bidirectional LSTM is an extension of traditional LSTMs that improves sequence learning by processing input data in two directions. It duplicates the hidden layer, allowing the model to accept information from both the past (forward) and the future (backward) contexts simultaneously.

* **Layer Configuration:**
  * **First Bi-LSTM Layer:** Contains 64 bidirectional units configured to return sequences so the next temporal layer can process it.
  * **Regularization:** A Dropout layer to control model complexity and prevent overfitting.
  * **Second Bi-LSTM Layer:** Contains 32 bidirectional units to further process the combined forward/backward contexts.
  * **Output Layer:** A final dense layer utilizing a **Sigmoid** activation function for binary classification.
* **Training Details:** Compiled with the **Adam optimizer** and **Binary Cross-Entropy loss**, trained for 30 epochs with a batch size of 32.
* **Performance:** Achieved a moderate testing accuracy of **65%**. While theoretically more powerful, its higher complexity likely led to slight overfitting due to the limited dataset size (300 total samples).

---

### 3. Random Forest Classifier
The Random Forest is a traditional, ensemble machine learning algorithm that builds a "forest" of multiple decision trees during its training phase. It combines their individual outputs using majority voting to determine the final classification.

* **Configuration:** * Implemented using `100 estimators` (100 independent decision trees).
  * Rather than processing frames sequentially, the sequential input matrix is flattened into a single vector of 3,960 features (`30 frames × 132 features`) per video.
* **Performance:** Achieved a baseline accuracy of **63%**. While computationally light, fast to train, and robust with high-dimensional data, it lacks the structure to capture the temporal motion or frame-to-frame sequence shifts inherent in a fight scene.


## Dataset
[Download the dataset used in this experiment from here !](https://github.com/seymanurakti/fight-detection-surv-dataset)

## Trained Models:
[Download the trained models generated in this project here !](https://drive.google.com/drive/folders/1-ChCXGILZO1btX4P2XTTB_7Q_NlW1gry?usp=sharing)

## 🚀 How to Use This Repository

### 1. Clone the Repository
To get a local copy of this project up and running on your desktop, open Git Bash or your terminal and run:
```bash
git clone [https://github.com/YOUR_GITHUB_USERNAME/Fight_Pose_Project.git](https://github.com/YOUR_GITHUB_USERNAME/Fight_Pose_Project.git)
cd Fight_Pose_Project
```
Install the necessary dependencies from the requirements.txt file.
```bash
pip install -r requirements.txt
```
Run the provided Jupyter notebooks to preprocess the data, train models, and make predictions.

After downloading the repository, :
```bash
Fight_Pose_Project
├── .git                                 # Hidden Git tracking repository folder
├── architecture_diagrams                # Directory containing model flow diagrams
│   ├── bi_lstm_model.png                # Architecture flow for the Bidirectional LSTM network
│   ├── lstm_model.png                   # Architecture flow for the standard LSTM network
│   └── random_forest.png                # Structural diagram for the flattened Random Forest baseline
│
├── Data                                 # Data management directory
│   ├── Raw                              # Video clips categorized by activity scenario (Fight vs. No Fight)
│   └── Poses                            # Extracted coordinates tracking human joint movements
│
├── models                               # Saved weights and parameters for compiled models
│   ├── bi_lstm_model.h5                 # Trained and serialized Bidirectional LSTM model
│   ├── fight_detection_lstm.h5          # Trained and serialized standard LSTM model
│   └── random_forest_model.pkl          # Pickled baseline Random Forest classifier model
│
├── data_preprocessing.py                # Script for skeleton tracking, zero padding, and video downsampling
├── train_models.py                      # Python pipeline script to compile and train ML/DL models
├── test_prediction.py                   # Prediction evaluation module for classifying new input sequences
├── requirements.txt                     # Text file specifying exact development dependencies and libraries
└── README.md                            # Main markdown repository project documentation page
```


## 📊 Evaluation Results

| Model | Training Accuracy | Validation Accuracy |
| :--- | :--- | :--- |
| LSTM Model | 0.7016 (70.16%) | 0.75 (75%) |
| Bi-LSTM Model | 0.6179 (61.79%) | 0.65 (65%) |
| Random Forest Classifier | 0.95 (95%) | 0.63 (63%) |


## Workflow of Model
<img src="https://github.com/Karthikkosuri/Human_Pose-Driven_Fight_Detection-/blob/main/Architecture%20Diagrams/work%20flow%20diagram.drawio.png?raw=true" alt="Project Diagram" width = "800"/>

## 🏁 Conclusion & Future Work

### Summary of Findings
This project successfully demonstrated the effectiveness of utilizing pose-based feature extraction for automated violence and fight detection in video surveillance sequences. By analyzing spatial-temporal arrangements of human skeletal joints rather than raw pixels, the system offers a lightweight, resource-efficient alternative to traditional computationally heavy surveillance models. 

Key architectural takeaways from this study include:
* **LSTM Networks** proved to be the most superior model, achieving a peak validation accuracy of **75%**. This underscores the vital importance of capturing sequence dynamics and sequential dependencies across sequential frames for high-accuracy action recognition.
* **Bi-LSTM Networks** achieved a moderate validation accuracy of **65%**. While theoretically better equipped for contextual pattern matching in both directions, its complex bidirectional structure was prone to slight overfitting due to dataset sample sizing constraints.
* **Random Forest Classifiers** provided a solid traditional baseline with **63%** validation accuracy. Despite handling high-dimensional spaces efficiently on a low computing threshold, it naturally falls short because it cannot natively learn the frame-to-frame temporal motion paths critical to evaluating complex physical interactions.

---

### ⚠️ Current Limitations
While the results are promising for automated security frameworks, the project highlights several key challenges:
1. **Quality of Pose Estimation:** The framework heavily depends on the consistency of the upstream keypoint extraction. Imprecise tracking caused by camera occlusion, fast-paced motion blur, or poor ambient lighting directly shifts or drops vital keypoints.
2. **Dataset Scale constraints:** The model was trained on a restricted pool of 300 total video samples (150 fight / 150 non-fight events). This limited size restricts the structural generalization boundaries of the deep learning layers.
3. **Sequence Length Fixed Uniformity:** Uniformly sizing all inputs to exactly 30 frames means shorter sequences relied on zero-padding while longer streams were downsampled, which might skip or drop fine-grained action anomalies.
4. **Scene Semantic Depth:** The model focuses purely on individual skeletal coordinate variations in isolation, missing deep environment semantics, multiple participant clusters, and chaotic background contexts found in real-world scenarios.

---

### 🚀 Future Research Directions
To build upon this foundation and transform it into a production-grade surveillance tool, future iterations will focus on:
* **Expanding Datasets:** Integrating larger scale public benchmarks (such as the UBI-Fights or Movie Fights datasets) to improve the feature robustness and overall generalization capabilities of the sequential deep learning models.
* **Hybrid Multimodal Architectures:** Fusing structural pose-tracking matrices alongside raw optical flow or spatial vision models (like 3D CNNs) to unify motion context, environmental semantics, and human interaction cues.
* **Adaptive Sampling:** Implementing modern dynamic padding or temporal segmentation algorithms to capture fluid frame patterns without risking key frame drops.

## Authors

- [@Karthikkosuri](https://github.com/Karthikkosuri)
