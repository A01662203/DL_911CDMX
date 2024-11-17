# Multimodal Model for Predicting 911 Call Nature

## Overview
The current model architecture aims to predict the nature of a 911 call using spatial, temporal, and categorical data. It is built with a multimodal approach, combining a Convolutional Neural Network (CNN) to extract spatial patterns, a Long Short-Term Memory (LSTM) network to capture temporal patterns, and an embedding layer to handle categorical features. Below is a detailed description of each part of the model's architecture and its components.

## Model Components

### 1. Spatial Input - CNN
The spatial input consists of a 10x10 grid matrix representing the normalized geographic location of each call.
- **Conv2D**: A convolutional layer with 8 filters and a 3x3 kernel. This layer is designed to extract spatial features, such as geographic distribution patterns of the calls.
- **MaxPooling2D**: A 2x2 pooling layer that reduces the spatial dimensionality and helps generalize detected patterns.
- **Flatten**: The output is flattened to prepare the data for concatenation.

### 2. Temporal Input - LSTM
The temporal input is a sequence of length 24, which includes normalized variables such as hour, day of the week, month, and latitude and longitude coordinates.
- **LSTM**: An LSTM layer with 16 units to capture dependencies over time in the sequential data. This layer is used to learn complex temporal relationships.

### 3. Categorical Embeddings - `categoria_incidente_c4`
The categorical input is the incident category, mapped to integer indices and represented via embeddings.
- **Embedding**: An embedding layer with an output of 8 dimensions that transforms categorical data into dense vectors, helping to represent categories in a way that can be interpreted by the model.

### 4. Concatenation and Dense Layers
- **Concatenation**: The output of the CNN, LSTM, and embeddings are concatenated to form a unified representation.
- **Dense**: A dense layer with 16 units that applies a non-linear transformation on the concatenated representation to combine information from different input types.
- **Dropout**: A Dropout layer with a rate of 0.3 to prevent overfitting by randomly dropping neurons during training.

### 5. Output Layer
- **Dense (Output)**: A dense layer with 5 units and `softmax` activation to predict the multiclass classification of each call's closure code ("Affirmative", "Informative", "Negative", "Duplicate", or "False").

## Model Training
- The model is compiled with the `Adam` optimizer and `categorical_crossentropy` loss due to the multiclass nature of the target.
- Callbacks such as `ReduceLROnPlateau` are used to reduce the learning rate when the validation loss stabilizes, helping to avoid getting stuck in local minima and improving convergence.
- Dropout configuration and L2 regularization in some layers are used to reduce overfitting, although the model still shows signs of overfitting.

## Observed Issues
- **Overfitting**: Despite several adjustments, the model continues to show high accuracy on training data and lower accuracy on validation data, indicating overfitting.
- **Model Complexity**: The model appears to be too complex given the nature of the available data, which may be contributing to the overfitting.

## Future Recommendations
- **Simplify the Architecture**: Reducing the number of dense layers or decreasing the size of some convolutional and LSTM layers could help reduce model capacity and improve generalization.
- **Additional Regularization**: Exploring other techniques such as `L1` regularization or applying greater `L2` penalties to the dense layers might help.
- **Increase Dataset Size**: If possible, increasing the dataset with additional data or using augmentation techniques could help improve the model's performance.


Enlace con los archivos:
https://drive.google.com/drive/folders/1LJfNajfbItxn2gAf5bxng_1ngm_01EcJ?usp=sharing