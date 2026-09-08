# Handwritten Digit Recognition Using CNN

A deep-learning project that recognizes isolated handwritten digits using a Convolutional Neural Network (CNN).

The notebook trains and evaluates a CNN on the MNIST handwritten-digit dataset, then exports the trained model and class labels for future inference.

## Project Overview

This project follows an end-to-end image-classification workflow:

```text
MNIST Dataset
    ↓
Image Preprocessing
    ↓
CNN Training and Validation
    ↓
Test Evaluation
    ↓
Classification Report and Confusion Matrix
    ↓
Sample Prediction
    ↓
Model Export
```

## Objectives

- Load the MNIST handwritten-digit dataset.
- Visualize sample digit images.
- Normalize image pixels and prepare image tensors for CNN input.
- Build and train a CNN classifier.
- Track training and validation accuracy and loss.
- Evaluate the trained model on the test set.
- Generate a classification report and confusion matrix.
- Visualize incorrectly classified examples.
- Export the trained model and digit class labels.
- Demonstrate prediction on an individual test image.

## Dataset

The notebook uses the MNIST dataset through TensorFlow/Keras:

```python
keras.datasets.mnist.load_data()
```

MNIST contains grayscale images of handwritten digits from `0` to `9`.

The notebook uses the dataset’s predefined training and test sets. The CNN is configured for 28 × 28 grayscale images, with one channel per image.

## Preprocessing

The images are preprocessed as follows:

- Pixel values are converted to `float32`.
- Pixel values are normalized from the `0–255` range to `0–1`.
- A channel dimension is added so images have the shape:

```text
(samples, 28, 28, 1)
```

## CNN Architecture

The model is built with TensorFlow/Keras using a sequential CNN architecture:

```text
Input: 28 × 28 × 1
    ↓
Conv2D: 32 filters, 3 × 3, ReLU
    ↓
Max Pooling: 2 × 2
    ↓
Conv2D: 64 filters, 3 × 3, ReLU
    ↓
Max Pooling: 2 × 2
    ↓
Dropout: 0.25
    ↓
Flatten
    ↓
Dense: 128 units, ReLU
    ↓
Dropout: 0.50
    ↓
Dense: 10 units, Softmax
```

The model is compiled with:

- Optimizer: Adam
- Loss function: Sparse categorical cross-entropy
- Metric: Accuracy

## Training

The CNN is trained with:

- Validation split: 10% of the training data
- Maximum epochs: 10
- Batch size: 128
- Early stopping monitored on validation loss
- Early-stopping patience: 2 epochs
- Best validation weights restored after training

The notebook plots both training and validation accuracy, as well as training and validation loss.

## Evaluation

The trained model is evaluated on the MNIST test set.

The notebook produces:

- Test loss
- Test accuracy
- Classification report
- Confusion matrix
- Visual examples of incorrect predictions

No fixed performance values are stated here, since results depend on the executed training run.

## Model Export

The notebook saves the trained CNN model and digit labels in an `exports/` directory:

```text
exports/
├── handwritten_digit_cnn.keras
└── class_labels.joblib
```

The `.keras` file contains the trained neural-network model, while `class_labels.joblib` stores the digit labels from `0` to `9`.

## Sample Prediction

The notebook demonstrates inference using one image from the test set. It displays:

- The input digit image
- Actual digit label
- Predicted digit label
- Prediction confidence

## How to Run

### Google Colab

1. Upload or open `Handwritten_Character_Recognition_CNN_Colab.ipynb` in Google Colab.
2. Run the cells in order.
3. Use the final download cell to download the exported `.keras` model.

### Local Environment

1. Clone this repository.

```bash
git clone https://github.com/your-username/handwritten-digit-recognition-cnn.git
cd handwritten-digit-recognition-cnn
```

2. Create and activate a virtual environment.

```bash
python -m venv venv
source venv/bin/activate
```

On Windows:

```bash
venv\Scripts\activate
```

3. Install dependencies.

```bash
pip install -r requirements.txt
```

4. Open and run the notebook in a notebook-compatible Python environment.

## Project Structure

```text
handwritten-digit-recognition-cnn/
├── Handwritten_Character_Recognition_CNN_Colab.ipynb
├── exports/
│   ├── handwritten_digit_cnn.keras
│   └── class_labels.joblib
├── requirements.txt
└── README.md
```

## Technologies Used

- Python
- TensorFlow / Keras
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- Joblib
- Google Colab or a notebook-compatible environment

## Limitations and Scope

This notebook recognizes isolated handwritten digits only.

Although the notebook discusses EMNIST as a possible extension for alphabet recognition, EMNIST loading and training are not implemented. Recognizing complete words or sentences would require additional steps such as character segmentation and sequence recognition.
