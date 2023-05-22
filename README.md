# Emergency Detection Based on Sound

## Introduction

The project is about detecting emergency sounds such as ambulance, police car, fire truck, etc. The main purpose of this project is to determine what features are important for emergency sound detection and how to use these features to detect emergency sounds, without using any deep learning methods.

## Dataset

The dataset is from [Emergency Vehicle Siren Sounds](https://www.kaggle.com/datasets/vishnu0399/emergency-vehicle-siren-sounds). It contains total 600 audio files, 400 for emergency consisting of ambulance and fire truck sirene, and 200 for non-emergency consisting of traffic sound. The audio files are in .wav format and each file is 3 seconds long. In order to improve the detection diversity, I added 400 more audio files for non-emergency sound from [Environmental Sound Classification 50](https://www.kaggle.com/datasets/mmoreaux/environmental-sound-classification-50). The audio files are in .wav format and each file is 5 seconds long. Besides that, I also augmented the dataset by adding white noise, shift, and stretch to the original audio files. Resulting in 4000 audio files in total, 1600 for emergency and 2400 for non-emergency.

## Feature Extraction

At first, I extracted most of the features possible from librosa library, which includes:

1. Zero Crossing Rate (ZCR)
2. Root Mean Square (RMS) Energy
3. Spectral Centroid
4. Spectral Bandwidth
5. Spectral Rolloff
6. Chroma Frequencies
7. Mel-Frequency Cepstral Coefficients (MFCCs)
8. Mel-Scaled Spectrogram
9. Spectral Contrast
10. Tonnetz

Then, I used the feature selection method to select the most important features. The result shows that the most important features are:

1. RMS Energy
2. Chroma Frequencies
3. Spectral Contrast (only the 4th and 5th contrast)

## Classification

I used 5 different classifiers to classify the audio files, which are:

1. Logistic Regression
2. Decision Tree
3. Random Forest
4. Support Vector Machine
5. Naive Bayes

All the classifiers are trained with the same training set and tested with the same testing set by also using K-fold cross validation to validate the result. The result are shown below:

| Classifier             | Cross Validation Accuracy | Testing Accuracy |
| ---------------------- | ------------------------- | ---------------- |
| Random Forest          | 0.966875                  | 0.97250          |
| Decision Tree          | 0.950312                  | 0.96250          |
| Support Vector Machine | 0.942812                  | 0.94875          |
| LogisticRegression     | 0.915312                  | 0.91375          |
| Naive Bayes            | 0.824687                  | 0.82625          |

## Conclusion

The result shows that the Random Forest classifier has the best performance. The reason might be that the Random Forest classifier is an ensemble classifier, which means it combines multiple decision trees to make a prediction. Therefore, it is more accurate than a single decision tree. The result also shows that the most important features are RMS Energy, Chroma Frequencies, and Spectral Contrast. Roughly, the reason behind this might be that these features are the most different between emergency and non-emergency sounds. For example, the RMS Energy of emergency sounds is higher than non-emergency sounds, and the Chroma Frequencies of emergency sounds are less concentrated and lower than non-emergency sounds. Condsidering that this detection is trained by very limited data and only using traditional machine learning methods, the result is quite good. However, the result can be improved by using larger and more diverse dataset, and also using deep learning methods.

## Reference

1. [Emergency Vehicle Siren Sounds](https://www.kaggle.com/datasets/vishnu0399/emergency-vehicle-siren-sounds)
2. [Environmental Sound Classification 50](https://www.kaggle.com/datasets/mmoreaux/environmental-sound-classification-50)
