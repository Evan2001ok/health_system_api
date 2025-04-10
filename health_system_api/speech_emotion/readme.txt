# Instructions for using the ONNX model for speech emotion recognition

This project is based on the open source project [Speech-Emotion-Analyzer](https://github.com/MiteshPuthran/Speech-Emotion-Analyzer). It significantly improves the model accuracy through feature engineering and data enhancement technology, and converts the model to ONNX format for easy deployment and use.

# Model performance

- Original model accuracy: 70%
- Improved model accuracy: 89%
- ONNX model accuracy: 92.50%


# files introduction

enhanced_feature_extraction.py is used for data preprocessing, and then train_improved_model.py is used for training. After training, h5_to_onnx.py is used to convert data into onnx format for easy deployment. emotion_recognition_inference.py is a local test plug-in designed by me to ensure the usability of the model.

# Emotion labels

The model can identify the following 10 emotion labels:

0. female_angry
1. female_calm
2. female_fearful
3. female_happy
4. female_sad
5. male_angry
6. male_calm
7. male_fearful
8. male_happy
9. male_sad

# requirements

- Python 3.6+
- Dependent libraries:

- numpy
- librosa
- onnxruntime
- matplotlib
- scikit-learn

You can install dependencies with the following command:

pip install numpy librosa onnxruntime matplotlib scikit-learn

## Usage

# Modify the prediction file path
# Initialize the emotion recognizer
model_path = "models/improved_model.onnx"
recognizer = EmotionRecognizer(model_path)

# Predict the emotion of the audio file
audio_file = "path/to/your/audio.wav"
emotion, probabilities = recognizer.predict_file(audio_file)

## Feature extraction instructions

This model uses a combination of multiple audio features, including:

1. MFCC features (n_mfcc=40)

2. Chroma features

3. Mel spectrum

4. Spectral centroid

5. Spectral bandwidth

6. Spectral contrast

7. Spectral flatness

8. Zero crossing rate

For each feature, the mean, standard deviation, maximum and minimum statistics are calculated to form a 764-dimensional feature vector.

## Model improvement methods

1. **Feature engineering**:
- Expand from a single MFCC feature to 8 audio features
- Calculate statistics for each feature to capture more information

2. **Data enhancement**:
- Add random noise
- Time stretching
- Pitch change

## Notes

#Audio files should be in WAV format with a sampling rate of 44.1kHz

# The best audio length is 3 seconds. If the audio is too long, only the first 3 seconds will be used

# The best recording function of pyaudio
