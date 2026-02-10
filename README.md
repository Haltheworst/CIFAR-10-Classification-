# ICSSR Research Submission: Track 2 - CIFAR-10 Image Classification
## Project: CIFAR-10 image classification

**Author:** Praket Kumar P

---

### 1. Project Overview
This repository presents a comparative study between a custom 3-layer Baseline CNN and an optimized ResNet-18 architecture to evaluate the impact of residual learning on image classification. The project demonstrates how Transfer Learning and Skip-Connections overcome the performance limitations of shallow networks, achieving a significant jump from 66% to 82% accuracy on the CIFAR-10 dataset.

### 2. Methodology & Reported Metrics
* **Train/Validation Split Method:** I utilized a randomized 90/10 split on the 50,000 training images, resulting in **45,000 images for training** and **5,000 for validation** to monitor generalization during every epoch.
* **Reported Metrics:** To ensure a comprehensive evaluation, I report **Accuracy**, **Precision**, **Recall**, and **F1-Score** for all classes.
* **Robustness Measures:** Implemented **Data Augmentation** (Horizontal Flips & Random Rotations) to ensure the model remains fair and invariant to object orientation.

### 3. Best Result Achieved
* **Top Performance Model:** Improved ResNet-18 (Transfer Learning).
* **Best Validation Accuracy:** **82.35%**.
* **Best Weighted F1-Score:** **0.82**.
* **Training Time:** 10 Epochs (~8 minutes on T4 GPU).

### 4. Architecture Comparison & Performance Analytics
| Feature | Baseline CNN | Improved Model (ResNet-18) |
| :--- | :--- | :--- |
| **Strategy** | Custom 3-Layer Architecture | Transfer Learning (Pre-trained) |
| **Optimization** | Adam (lr=0.001) | Adam (lr=0.0001) |
| **Peak Accuracy** | ~66% | **82.35% (Best Result)** |


#### Technical Insights & Optimization
* **Architecture Choice:** I utilized **ResNet-18** because its residual "skip-connections" prevent the vanishing gradient problem, allowing the model to learn more complex features than the custom baseline.
* **Optimizer Selection:** I chose the **Adam Optimizer** because of its adaptive learning rate capabilities, which allow for faster convergence compared to standard SGD.
* **Criterion:** **Cross-Entropy Loss** was implemented to effectively penalize incorrect high-confidence predictions in a multi-class environment.
* **Learning Rate Strategy:** A lower learning rate (0.0001) was applied to the ResNet-18 to ensure stable **fine-tuning** of pre-trained weights.
* **Hardware Efficiency:** A Batch Size of 64 was utilized to balance GPU memory efficiency with gradient stability.

#### Identified Constraints & Future Improvements
* **Inter-class Similarity:** The model exhibits confusion between visually similar classes, specifically **Cats vs. Dogs** (161 instances) and **Cars vs. Trucks** (79 instances).
* **Overfitting:** A slight gap between training and validation accuracy suggests the model is beginning to memorize training samples.
* **Future Work:** Implementing **Cosine Annealing** schedulers and **Early Stopping** to reach 90%+ accuracy.

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

### 5. Confusion Matrix & Key Findings
To evaluate reliability, I utilized a Confusion Matrix to identify specific inter-class biases and ensure system transparency.

![Confusion Matrix](confusion%20matrix.png)

* **High-Confidence Domains:** The model is exceptionally reliable for logistics categories, specifically **Trucks (904 correct)** and **Cars (888 correct)**.
* **Accountability Gap:** The significant failure point between **Cats and Dogs (161 instances)** highlights the need for **"Human-in-the-loop" verification** in high-stakes governance applications to maintain citizen trust.

### 6. Technical Disclosures
* **AI Assistance:** Generative AI was utilized to draft boilerplate documentation and refine the Markdown structure for this README.
* **Code Origin:** All core training logic and architectural modifications were implemented and verified through iterative testing on Google Colab.
* **Compute:** Training was performed using a **Tesla T4 GPU**.

### 7. How to Run
1. **Environment Setup:** Ensure dependencies are installed: `pip install -r requirements.txt`.
2. **Open Notebook:** Open `CIFAR_10_Praket.ipynb` in Google Colab.
3. **Hardware:** Set Runtime to **T4 GPU**.
4. **Execution:** Run all cells to reproduce results.
*Note: Due to GitHub's file size limitations, the .pth model weights are stored locally but can be provided upon request.*
