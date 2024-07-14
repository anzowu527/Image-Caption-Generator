# Image-Caption-Generator

## Introduction:

- Objective: Create a model that generates text descriptions from image data.
- Applications: Accessibility for visually impaired, assistive technology, and real-time scene descriptions.
- Dataset: Used the Flickr_8k dataset from Kaggle, containing 8000 images each paired with five unique captions.

## Data Preparation:
Caption Text Preprocessing:
- Removed punctuation and converted text to lowercase.
- Eliminated words containing numbers.
- Tokenized text, mapping each unique word to a numeric value.
- Appended '<start>' and '<end>' identifiers to each caption.

Image Data Preprocessing:
- Resized and normalized images to a consistent format.
- Applied image augmentation techniques (rotation, zoom, flipping).
- Experimented with color space conversions (RGB to HSV, grayscale).
- Applied noise reduction techniques (Gaussian blur, median filtering).

## Pre-Modeling Data Transformation:

Feature Extraction for Images:
- Xception Model: Pretrained on ImageNet, removed last fully connected layer, obtained 2048-dimensional feature vectors.
- ResNet50 Model: Pretrained on ImageNet, utilized residual blocks, obtained feature vectors for 224 × 224 pixels images.
- VGG16 Model: Sequentially stacked convolutional layers, used small 3 × 3 filters, captured detailed spatial information.

Model Comparison: Found Xception slightly better in performance, ResNet50 quickest in extraction time, VGG16 slowest.

## CNN-RNN Model Structure:

- Feature Extractor: Used Xception to extract relevant features from images, reduced dimensionality to 256.
- Sequence Processor: Combined image embeddings with word embeddings, fed into an LSTM layer to generate next word.
- Decoder: Merged outputs from feature extractor and sequence processor, predicted final word probabilities.

## Evaluation Metric and Results:

- BLEU Score: Incorporated BLEU score for evaluating model performance in generating appropriate captions.
- Training Process: Implemented BLEU score as a callback metric, faced challenges due to dataset size, conducted one-time evaluation with selected image samples.
