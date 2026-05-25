# Human Pose-Driven Fight Detection Using Random Forest and LSTM Architectures

## 📌 Project Description
This project focuses on developing an automated, lightweight violence detection system for real-time video surveillance. Instead of analyzing heavy, raw pixel data which often leads to high false-positive rates, this approach extracts 132 spatial coordinates representing human skeletal keypoints (66 body joints per frame) to model structural and physical interactions. 

To classify actions into "fight" or "no fight" categories, the project implements and evaluates three distinct models:
* **Long Short-Term Memory (LSTM):** Captures temporal relationships across consecutive frames, delivering the highest overall accuracy of **75%**.
* **Bidirectional Long Short-Term Memory (Bi-LSTM):** Analyzes sequence patterns in both forward and backward directions, yielding a moderate accuracy of **65%** due to dataset constraints.
* **Random Forest Classifier:** Used as a traditional, computationally light machine learning baseline, achieving an accuracy of **63%** but failing to capture sequence changes over time.

Ultimately, this project demonstrates that utilizing sequential deep learning models to track human pose dynamics provides an efficient, low-resource solution for automated security monitoring without requiring high-end computing setups.
