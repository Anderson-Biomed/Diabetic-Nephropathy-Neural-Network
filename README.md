# Diabetic Nephropathy Neural Network

## Overview

This project uses a simple neural network to predict **diabetic nephropathy** from clinical data.

The notebook covers data preparation, feature encoding, scaling, model training, evaluation, and visualization of the results.

## Dataset

The dataset contains **133 patients** and 15 variables related to clinical characteristics, metabolic measurements, treatment, and blood pressure.

Some of the variables include:

- Sex
- Age
- BMI
- Diabetes type
- Diabetes duration
- Fasting blood sugar (FBS)
- HbA1c
- LDL
- HDL
- Triglycerides
- Treatment
- Systolic blood pressure
- Diastolic blood pressure

The target variable is `NEFRO`, which represents diabetic nephropathy status.

## Workflow

The notebook follows these main steps:

1. Load the clinical dataset.
2. Encode categorical variables.
3. Separate predictors from the target variable.
4. Standardize the input features using `StandardScaler`.
5. Split the data into training and test sets.
6. Build and train a neural network.
7. Evaluate the model using accuracy and AUC.
8. Visualize the training process and model performance.
9. Examine correlations between the clinical variables.
10. Generate predictions for example patient profiles.

## Neural Network

The final model is a fully connected neural network implemented with Keras.

```text
Input
   ↓
Dense (128) + L2 regularization
   ↓
LeakyReLU
   ↓
Dropout (0.3)
   ↓
Dense (128) + L2 regularization
   ↓
LeakyReLU
   ↓
Dropout (0.4)
   ↓
Dense (64) + L2 regularization
   ↓
LeakyReLU
   ↓
Dense (32) + L2 regularization
   ↓
LeakyReLU
   ↓
Dense (1) + Sigmoid
```

## Why These Methods Were Used

### Data preprocessing

**Categorical encoding**

Categorical variables such as `SEXO` (Gender) and `TRAT` (Treatment) were transformed into numerical representations so they could be used as inputs to the neural network.

**StandardScaler**

The numerical features were standardized before training. This puts the variables on a comparable scale and is useful when the model receives clinical measurements with very different ranges.

**Train/test split**

The data was divided into training and test sets to train the model on one portion of the data and evaluate its performance on unseen samples.

### Model architecture

**Dense layers**

Fully connected layers were used to learn nonlinear relationships between the clinical variables and the presence of diabetic nephropathy.

**LeakyReLU**

LeakyReLU was used as the activation function in the hidden layers to introduce nonlinearity while maintaining a small gradient for negative inputs.

**L2 regularization**

L2 regularization was included in the Dense layers to penalize large model weights and help reduce overfitting.

**Dropout**

Dropout was used to randomly deactivate part of the network during training. This adds another form of regularization and can help reduce overfitting.

**Sigmoid output**

The final layer uses a sigmoid activation because the task is binary classification: predicting whether diabetic nephropathy is present or not.

### Training

**Adam optimizer**

Adam was used to update the model weights during training. The learning rate was set to `0.0005`.

**Binary cross-entropy**

Binary cross-entropy was selected as the loss function because the model performs binary classification.

**Early stopping**

Training could run for up to 200 epochs, but `EarlyStopping` monitored validation AUC and stopped training when the model stopped improving. The best weights were then restored.

### Evaluation

**Accuracy**

Measures the proportion of predictions that were classified correctly.

**AUC**

AUC was included to evaluate the model's ability to distinguish between the two classes across different classification thresholds.

**Confusion matrix and ROC curve**

These visualizations were used to examine classification performance in more detail and to understand the model's behavior beyond accuracy alone.
