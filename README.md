# Quantum vs Classical Feature Selection

## Overview

This repository contains two experiments that compare classical and quantum-inspired feature-selection techniques under noisy input conditions. The aim is to study their classification performance, feature-selection behaviour and computational cost.

Both experiments use the **Breast Cancer Wisconsin dataset** from Scikit-learn. Gaussian noise is introduced during feature selection, while the selected features are evaluated using clean data.

## Experiments

### 1. RFE vs QSVM-RFE

This experiment compares two Recursive Feature Elimination (RFE) approaches:

- **Classical RFE (RBF-SVM):** Uses a Support Vector Machine with a Radial Basis Function kernel to evaluate feature importance.
- **QSVM-RFE (ZZFeatureMap):** Uses a quantum kernel based on Qiskit's ZZFeatureMap to evaluate feature importance.

Both methods use permutation importance to rank features. At each iteration, the feature with the smallest contribution is removed until the required number of features remains.

The quantum kernel is constructed using exact statevector simulation, with fidelity between quantum states used to calculate the kernel matrix.

**Evaluation metrics:**
- Training hinge loss
- Test accuracy
- F1-score
- Feature-selection execution time

### 2. Random Walk vs Quantum Walk

This experiment compares classical Random Walk and a simulated Quantum Walk approach for selecting features.

The process begins by constructing a QUBO (Quadratic Unconstrained Binary Optimization) matrix from the noisy training data.

- **Classical Random Walk:** Uses a Markov chain and a row-normalised transition probability matrix to calculate feature visit probabilities.
- **Quantum Walk (Qiskit):** Uses a spectral simulation based on the discriminant matrix and eigenvalue decomposition to simulate quantum-walk-inspired probability evolution.

Both methods operate on the same feature graph. Features are ranked according to their accumulated probabilities, and the top-k features are selected.

**Evaluation metrics:**
- QUBO energy
- Test accuracy
- Execution time
- Comparison with the brute-force optimal QUBO energy

## Dataset

The experiments use the Breast Cancer Wisconsin dataset available through `sklearn.datasets.load_breast_cancer()`.

- Total samples: 569
- Total features: 30
- Classification: Binary (Malignant and Benign)

Different feature-space sizes are considered:

`N = [4, 8, 12, 15]`

The target number of selected features is approximately half of the available features.

## Experimental Setup

The following settings are used in both experiments:

| Parameter | Value |
|---|---|
| Dataset | Breast Cancer Wisconsin |
| Train-test split | 70:30 |
| Number of random seeds | 10 |
| Gaussian noise standard deviation | 0.05 |
| Feature sizes | 4, 8, 12, 15 |
| Data scaling | StandardScaler |
| Evaluation | Clean test data |

The experiments use the same random seeds and data splits for both methods within each comparison.

Results are reported as mean ± standard deviation across the ten runs.

## Technologies Used

- Python
- NumPy
- Pandas (optional for additional analysis)
- Matplotlib
- Scikit-learn
- Qiskit
- Qiskit Aer

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/your-repository.git
cd your-repository
```

Install the required libraries:

```bash
pip install numpy matplotlib scikit-learn qiskit qiskit-aer
```

## Running the Experiments

Run the first experiment:

```bash
python rfe_comparison.py
```

Run the second experiment:

```bash
python random_walk_comparison.py
```

*Replace the filenames with the actual names of your Python files if they differ.*

Both scripts print the experimental results and generate plots for comparing the methods.

## Implementation Notes

- Gaussian noise is added only during feature selection.
- The final classifier evaluation uses the original clean training and testing data.
- The same downstream classifier is used for both methods within each experiment.
- The first experiment uses an exact statevector-based quantum kernel simulation.
- The second experiment uses spectral simulation for quantum-walk-inspired probability evolution.

**Note:** Both quantum approaches are evaluated through classical simulation. Their execution times represent simulation costs and should not be interpreted as estimates of actual quantum hardware performance.

## Future Improvements

- Experiment with different Gaussian noise levels.
- Measure feature-selection stability across multiple runs.
- Evaluate the methods on additional datasets.
- Explore more complete quantum-walk implementations.
- Investigate other quantum-based feature-selection techniques.
- Improve computational efficiency for larger feature sets.

## Conclusion

This project provides a comparative study of classical and quantum-based feature-selection approaches under noisy input conditions. It examines their classification performance and computational requirements to understand how quantum-based methods compare with their classical counterparts.
