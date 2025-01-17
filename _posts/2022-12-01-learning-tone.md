---
title:  "Learning Human-Like Tonal Inflections for Humanoid Robotics"
mathjax: true
layout: post
categories: media
---

One important aspect of human interaction is communication through facial expressions and tones used within speech. Because of this, the ability to of a humanoid robot to achieve natural lip synchronization is critical to improving human-robot interactions. This project aims to explore these areas and specifically provides recommendations for improving both humanoid robots’ hardware and software to mimic human speech better. In the realm of this project, we aim to improve lip synchronization using machine learning methods to mechanically actuate human speech sounds and link the auditory and visual output.


## Procedure

### Background
Prior to establishing a baseline for experiments, it is important to discuss the audio preprocessing techniques used in the study. This begins with understanding the Fourier Transform, which decomposes a signal into its individual frequencies and amplitudes, thus converting the signal from the time to frequency domain. However, since most speech signals are non-periodic a Fast Fourier Transform is performed over several segments of the signal which then results in a spectrogram. This spectrogram provides a visualization of spectrum of frequencies over time. This spectrum of frequencies is, however, on a scale that doesn’t mimic the way humans hear sound, so the logarithmic transformation of a signal’s frequency, also known as the Mel Scale, aims to fix this problem. These Mel Scale Spectrograms are then converted to Mel Frequency Cepstral Coefficients (MFCCs), which are derived by applying a discrete cosine transformation. Once the audio is processed into a corresponding MFCC, it is only then that it may be used to train a neural network.

![MFCC](/assets/learn_tone_images/mfcc_example.jpg)

Fig: Example of a typical MFCC (Source: [Medium](https://medium.com/@tanveer9812/mfccs-made-easy-7ef383006040))

### Setup
The data for human speech used in this study were sourced from the Tone Perfect database which contains 410 monosyllabic sounds spoken in Mandarin Chinese each utilizing the four different tones of: high-level, rising, dipping, and falling. As for the robot audio recordings, a simple mouth and throat robot was used to replicate these tonal inflections. This robot consisted of a flexible silicon tube, with a mouth shaped opening at one end, that was deformable through a series of servo motors. These servo motors were tasked with altering the pathway of the air flowing through the silicon tube to achieve a range of tones for spoken words. In the scope of this project, the robot was only tasked with articulating the “ma” speech utterance to test the capabilities of the current system. In doing so, 280 attempted utterances were made for each tone under a possible range of predefined servo motor positions.

![Robot](/assets/learn_tone_images/mouth_robot.jpg)

Fig: Mouth Robot used in Experimentation

### Architecture
With the newly acquired robot speech, classification can now be done to determine how closely it was able to match human speech. The main architecture used in this study was just a simple CNN used to classify the four Mandarin tones that were previously mentioned. Specifically, the CNN consisted of three convolutional layers, one max pooling layer, and three corresponding fully connected layers with a SoftMax activation at the very end to classify what tone was just uttered. This simple architecture may have proved to be inefficient, however it was believed to be an appropriate model as it was used in previous works for solely classifying human speech tones on the same Tone Perfect database and produced highly accurate results.

![SimpleCNN](/assets/learn_tone_images/simple_cnn.jpg)
Fig: Simple CNN Architecture

### Experimentation
Once the architecture was developed, the first goal was to train the model on both the human and robot speech corpuses to determine if relevant information can be learned from the data. This was done because later when testing the model trained on human speech, on robot speech, it is critical that it fully understands the underlying features found in each tone for human speech. When training the model on solely human speech a test accuracy of 99.8% was achieved.  In conjunction with this, when training the model on solely robot speech a test accuracy of 94.2% was achieved. These high accuracies indicate that the model was capable of learning from the data provided. Now that benchmarks have been made on both datasets, proving the ability for the model to learn, the next step is to test if the model trained on human speech can classify robot speech. In doing so, the model produced a test accuracy of 25.8%. Specifically, the model categorized almost all the robot speech as a single tone, and when there are 4 total tones it resulted in only a quarter of the data being classified correctly.

### Results and Thoughts
With these results in mind, it indicates that the current hardware being used is limited in its ability to produce the full range of pitches that are found in human speech. This assumption is further supported by the large quantity of trials being classified as high-level. This tone is relatively unchanging across the sequence of time for the audio sample. Because of this it can be assumed that the samples from the robot are not producing significant changes in frequency and pitch and the model is just categorizing it as a relatively miniscule change resulting in it classifying the signal as high-level.

Following these results there are two proposed solutions for future work regarding this project. The first proposed solution is to update the current hardware specifically the current bagpipe reed that is being vibrated to produce the range of pitch as air is being passed through the silicon tube. Another proposed solution is utilizing reinforcement learning to optimize and maximize the capabilities of the current hardware. This can be accomplished by having the model learn the optimal changes in the servo motors to produce the highest score in producing any of the given tones. The agent in this experiment would be the robot itself and the possible actions are the angle to rotate each of the given servo motors at a predefined set of discrete timesteps. As for the reward, since the model trained on the human speech is exceptional at classifying the tones from humans, it can be utilized to classify each output from the agent and then provide a score that can simply be the confidence score of the classification of the tone following the SoftMax activation layer.
