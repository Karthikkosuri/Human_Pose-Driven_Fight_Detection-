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
