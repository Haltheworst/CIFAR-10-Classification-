# ICSSR Research Submission: Track 2 - CIFAR-10 Image Classification
## Project: CIFAR-10 image classification

**Author:** Praket  Kumar P
---

### 1. Project Overview
This repository presents a comparative study between a custom 3-layer Baseline CNN and an optimized ResNet-18 architecture to evaluate the impact of residual learning on image classification. The project demonstrates how Transfer Learning and Skip-Connections overcome the performance limitations of shallow networks, achieving a significant jump from 66% to 82% accuracy on the CIFAR-10 dataset.

### 2. Methodology & Data Strategy
* **Dataset:** CIFAR-10 (60,000 images, 10 classes).
* **Train/Validation Split:** A 90/10 split (45,000 train / 5,000 validation) was used to monitor generalization.
* **Robustness Measures:** Implemented **Data Augmentation** (Horizontal Flips & Random Rotations) to ensure the model remains fair and invariant to object orientation.

### 3. Architecture Comparison
| Feature | Baseline CNN | Improved Model (ResNet-18) |
| :--- | :--- | :--- |
| **Strategy** | Custom 3-Layer Architecture | Transfer Learning (Pre-trained) |
| **Optimization** | Adam (lr=0.001) | Adam (lr=0.0001) |
| **Peak Accuracy** | ~66% | **82.35%** |

### 4. Performance Analytics

The Improved Model reached a peak validation accuracy of **82.35%** in just 10 epochs using a T4 GPU.

#### Technical Insights & Optimization

* **Architecture Choice:** I utilized **ResNet-18** because its residual "skip-connections" prevent the vanishing gradient problem, allowing the model to learn more complex features than the custom baseline.
* **Optimizer Selection:** I chose the **Adam Optimizer** because of its adaptive learning rate capabilities, which allow for faster convergence on image datasets compared to standard Stochastic Gradient Descent (SGD).
* **Criterion:** **Cross-Entropy Loss** was implemented as the specific classifier objective, as it effectively penalizes incorrect high-confidence predictions in multi-class environments.
* **Learning Rate Strategy:** A lower learning rate (0.0001) was applied to the ResNet-18 to ensure stable **fine-tuning** of pre-trained weights, whereas the baseline used a higher rate (0.001) to learn from scratch.
* A Batch Size of 64 was utilized to balance GPU memory efficiency with gradient stability.

#### Identified Constraints & Future Improvements

While the model performs strongly, two main issues were observed:

* **Inter-class Similarity:** The model exhibits confusion between visually similar classes, specifically **Cats vs. Dogs** (161 instances) and **Cars vs. Trucks** (79 instances), due to shared spatial features and backgrounds.
* **Overfitting:** A slight gap between training and validation accuracy suggests the model is beginning to memorize training samples rather than generalizing.

**To reach 90%+ accuracy, future iterations should include:**

1. **Learning Rate Scheduling:** Implementing a **Cosine Annealing** scheduler to help the model settle into global minima.
2. **Extended Training:** Increasing the epoch count to 100+ while utilizing **Early Stopping** to prevent overfitting.
3. **Advanced Augmentation:** Incorporating **Random Cropping** and **Color Jittering** to force the model to learn more invariant features.



#### Learning Curves
![Base CNN Loss](Base%20CNN%20loss.png)
![Resnet Loss](Resnet%20loss.png)

#### Detailed Classification Report
The model achieved a **Weighted Average F1-Score of 0.82**.

| Class | Precision | Recall | F1-Score |
| :--- | :--- | :--- | :--- |
| **Ship** | 0.92 | 0.87 | 0.90 |
| **Car** | 0.91 | 0.88 | 0.89 |
| **Truck** | 0.88 | 0.89 | 0.88 |
| **Cat** | 0.73 | 0.59 | 0.65 |



### **5. Confusion Matrix & Key Findings**

To evaluate the model's reliability, I utilized a Confusion Matrix to identify specific inter-class biases. This provides a transparent view of where the model is highly "Accountable" and where it requires human oversight.
![Confusion Matrix](confusion%20matrix.png)

#### **Results Analysis**

* **High-Confidence Domains:** The model is exceptionally reliable for infrastructure and logistics categories, specifically **Trucks (904 correct)**, **Ships (882 correct)**, and **Cars (888 correct)**, all achieving precision scores above 88%.
* **The "Accountability Gap":** The most significant failure point occurs between **Cats and Dogs**, with **161 instances** of confusion. This indicates that while the model understands general animal features, it lacks the fine-grained distinction needed for biological accuracy in low-resolution contexts.
* **Infrastructure Confusion:** There is a notable overlap between **Cars and Trucks (79 instances)**. In a governance or smart-city application, such errors would necessitate a "Human-in-the-loop" verification step to maintain system trust and fairness.

### **6. Technical Disclosures**

In alignment with the principles of **Algorithmic Transparency**:

* **AI Assistance:** Generative AI was utilized to draft boilerplate documentation and refine the Markdown structure for this README.
* **Code Origin:** All core training logic, data pipeline configurations, and architectural modifications (ResNet-18 fine-tuning) were implemented and verified through iterative testing on Google Colab.
* **Compute:** Training was performed using a **Tesla T4 GPU** to ensure computational efficiency and reduced environmental footprint.

### 7. How to Run

1. **Environment Setup:** Ensure you have the necessary dependencies installed by running:
```bash
pip install -r requirements.txt

```
2. **Open Notebook:** Open `CIFAR_10_Praket.ipynb` in Google Colab or a local Jupyter environment.
3. **Hardware Acceleration:** Ensure Runtime is set to **T4 GPU** for optimal performance.
4. **Execution:** Run all cells to reproduce results and verify the saved model weights (`improved_model.pth`).
---
