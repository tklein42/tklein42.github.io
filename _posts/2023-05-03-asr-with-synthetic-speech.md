---
title:  "Automatic Speech Recognition with Synthetic Speech"
mathjax: true
layout: post
categories: media
---

A major hindrance to training high-performance automatic speech recognition systems is the collection of well-labeled and curated data, which up to this point has proven to be exceedingly expensive both in time and resources. This project aims to overcome this challenge by determining if automatic speech recognition systems that are solely trained on large amounts of synthetic speech perform at least as well as systems trained on actual human speech. In conjunction, this project also aims to identify the best mechanisms to produce a corpus of synthetic human speech that can rival that of actual human speech in speech recognition training. Successful synthesis could lead to the elimination of costs associated with data collection and curation, allowing for more resources to be directed toward the development and training of superior synthesis and recognition systems.


## Procedure

### Baseline

For the baseline evaluation of our experiments, we first chose appropriate models for both speech synthesis and recognition. The selection process needed to incorporate components such as ease of access and performance due to the timeline given and the resources available to train large, impressive models. For speech synthesis, a synthesizer known as VITS, or variational inference with adversarial learning for end-to-end text-to-speech, was chosen. This synthesizer enables the input transcripts of text to be spoken in a variety of different pitches and rhythms to replicate the many variations in human speech. A visualization of the VITS model architecture can be seen below.

![VITS](/assets/asr_synth_speech/VITS.png)

As for speech recognition, the recognizer LAS, or Listen, Attend, and Spell, was chosen. This recognizer was chosen for being well-documented and well-tested on the speech corpus, LibriSpeech. In conjunction with this, the model size and performance are also major considerations in model choice. For measuring performance two separate metrics were used. The first, WER, or Word Error Rate, is a common metric in speech recognition that measures the ratio of errors in a transcription to the total words spoken. When using this metric LAS provides a word error rate (WER) of 18.24, which is a satisfactory result without requiring the large amount of computation power to train state-of-the-art models. The second metric, LD, or Levenshtein Distance, is another common metric that is used to calculate the difference between two sequences. It accomplishes this by determining the number of single-character edits that are needed to make the two strings identical. When using this metric LAS returns an LD of 11 on the LibriSpeech Corpus, which similar to the WER is also satisfactory for proving the overall hypothesis. This decision seemed appropriate as the goal is to solely test whether synthetic data can achieve similar results to that of ASR systems trained on real data. A visualization of the LAS model architecture can be seen below.

![LAS](/assets/asr_synth_speech/LAS.png)

### Experimental Process

The first step in the experimental process is creating an identical corpus of LibriSpeech of entirely synthetic speech. This is accomplished by taking the transcripts from the train-clean-100, train-clean-360, dev-clean, and test-clean subsets and passing them through the pre-trained VITS synthesizer. This large amount of synthetic data allows for parsing of different sizes to be used during training. Then, the audio files were converted into the corresponding MFCCs, also known as Mel-frequency cepstral coefficients. This provides an effective method to extract features from the waveform and is directly used as the input for the LAS model being used. Once this was complete 3 separate models were trained using 100, 200, and 300 hours of synthetic speech.

### Results and Conclusion

As concluded from the initial experiments, each model trained achieved a good score on their corresponding validation sets. However, it was seen that a lot more synthetic data was necessary to approach the Levenshtein Distance achieved from just training on the real data. So much so that 300 hours of synthetic data only achieved an LD of 23.38 whereas the 100 hours of real data were capable of achieving an LD of 12.11, this was a surprising result as it brought up many questions regarding the quality of the synthetic data. 

After the initial results, the next testing stage consisted of cross-validating each of the trained models observing their performance on real data, and measuring the ability to generalize to human speech. From this, it was seen that the model trained on synthetic data showed a 5 times increase in WER and roughly 37 times increase in LD. Both of these metrics saw a similar trend as previously mentioned where both increased alongside the amount of synthetic data being used. This leaves much to be desired to compete with real-world data and the performance it gives. This result is likely due to the intricacies found within speech that are being replicated within the speech synthesizer. Since the amount of synthetic data shows a negative trend in performance with hours of synthetic data it can be assumed that the quality of synthetic data in comparison to the original real data is vastly different. This difference may not be distinguishable for the human ear but for training a speech recognizer this results in abysmal performance. Although this trend exists, further research must go into identifying the key features differentiating synthetic and real speech that may not be noticeable to humans.


