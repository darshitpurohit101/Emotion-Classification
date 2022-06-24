# Emotion-Classification

## Overview
This project was carried as a course project for the course Advanced Deep Learning at Eötvös Loránd University.

## Datasets
The [IEMOCAP](https://link.springer.com/content/pdf/10.1007%2Fs10579-008-9076-6.pdf) dataset was used for all the experiments in this work. 
## Code
1. extract emotion labels: extract labels from transriptions and compile other required data into a csv.
2. build audio vectors: build vectors from the original wav files and save into a pickle file
3. extract audio features: extract 8-dimensional audio feature vectors for the audio vectors
4. prepare data: preprocess and prepare audio data for experiments
5. train LSTMClassifier before running any other experiments for easy comparsion with other models
6. audio classification: train ML classifiers for audio

