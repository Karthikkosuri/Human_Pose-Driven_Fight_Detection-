# Human Pose-Driven Fight Detection Using Random Forest and LSTM Architectures

## 📌 Project Description
[cite_start]This project focuses on developing an automated, lightweight violence detection system for real-time video surveillance[cite: 20, 25]. [cite_start]Instead of analyzing heavy, raw pixel data which often leads to high false-positive rates, this approach extracts 132 spatial coordinates representing human skeletal keypoints (66 body joints per frame) to model structural and physical interactions[cite: 42, 72, 77, 86]. 

[cite_start]To classify actions into "fight" or "no fight" categories, the project implements and evaluates three distinct models[cite: 22, 54, 92]:
* [cite_start]**Long Short-Term Memory (LSTM):** Captures temporal relationships across consecutive frames, delivering the highest overall accuracy of **75%**[cite: 23, 36, 113, 161].
* [cite_start]**Bidirectional LSTM (Bi-LSTM):** Analyzes sequence patterns in both forward and backward directions, yielding a moderate accuracy of **65%** due to dataset constraints[cite: 23, 37, 119, 164].
* [cite_start]**Random Forest Classifier:** Used as a traditional, computationally light machine learning baseline, achieving an accuracy of **63%** but failing to capture sequence changes over time[cite: 23, 35, 96, 97].

[cite_start]Ultimately, this project demonstrates that utilizing sequential deep learning models to track human pose dynamics provides an efficient, low-resource solution for automated security monitoring without requiring high-end computing setups[cite: 24, 25, 139, 186].
