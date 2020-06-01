---
layout: page
title: Raga Classification
tagline: Quantifying and Analyzing Ragas in Indian Classical Music
description: Capstone proj
---
# Background
Indian Classical music contains two primary divisions - North Indian Classical (Hindustani), and South Indian Classical (Carnatic). While both styles have their fundamental differences, the underlying structure of styles can be captured in a raga/raag/ragam. A raga is defined as “a pattern of notes having characteristic intervals, rhythms, and embellishments, used as a basis for improvisation.” A raga can be compared to a type of scale in Western classical music. Though Western classical music does not have a direct equivalent to this concept, a raga is somewhat comparable to certain scales, such as a natural harmonic minor or a major scale. Every song has a raga that it is set to. For example, the raga Kirvani is equivalent to the natural harmonic scale in Western music.
Our goal with this project is to quantify ragas in a way that we can then build a raga identification tool. This tool would be able to “listen” to an audio clip and be able to identify the raga that the song is set to. It would mimic what seasoned listeners of Indian classical music do already: try to identify a raga while listening to music. By quantifying the features of a ragam, we will attempt to build a raga identification classifier. However, as noted by those who have attempted this in the past, “quantifying raga similarity becomes extremely challenging as it demands assimilation of both intrinsic (viz., notes, tempo) and extrinsic (viz. raga singing time, emotions conveyed) properties of ragas.” (Mishra 1) To manage the scope of this project with the time we have, we will build this tool to be functional for 10 prominent Hindustani/Carnatic ragas. These 10 prominent ragas are known as thaats. These are known as: 
- Asavari (Hindustani)/ Natabhairavi (Carnatic)
- Bilawal / Dheerashankarabharanam
- Bhairav / Mayamalavagowlai
- Bhairavi / Hanumatodi
- Kafi / Karaharapriya
- Kalyan / Kalyani
- Khamaj / Harikhamboji
- Marva / Gamanashama
- Poorvi / Kamarvardhani
- Todi / Shubhapantuvarali

# Data Cleaning
Indian classical music has a huge number of Ragas (Carnatic alone has upward of 30,000 ragas). Given the time and resources currently available to us, it would be impossible to incorporate each of those ragas into our analysis. Thus, we are focusing on 10 major ragas, thaats. Thaats are unique because each of them have the same notes in the ascending and descending scale and are not “missing” any notes (both ascending and descending scale contain the full 7 notes). While the ragas that we picked are just a starting point, they are also important and influential ragas in and of themselves (every Hindustani raga is a derivative of one of these 10 thaats). 

Once we narrowed down which ragas we would include in our analysis, we picked songs that were set to those ragas. Since these songs came from our personal collection, which includes mostly violin and vocal music, we used almost every song that we had that was set to the appropriate raga. 
In Indian classical music, each artist plays in a specific sruthi, which is a pitch that the first note in the scale of the raga (sa) is played from. To make sure we could correctly analyze the difference between multiple songs, we identified what pitch each song was in and shifted the pitch of every song to be in C Major. We also chunked each of our songs to be 45 seconds in length so that later in our analysis, we could more accurately extract notes from them. We then loaded this information (encoded as an audio time-series array) into a csv for further use.


# Analysis : Background
Thaat To Scale: 

![Thaat To Scale](https://raw.githubusercontent.com/sruthiv98/RagaClassifier/gh-pages/images/thaattoscale.jpeg)



Our analysis attempts to show the quantitative differences between each of the 10 ragas with starting ideas on how we may go on to use these differences when building a classifier. We aim to do this in two parts: the first will focus on the frequency of notes in each raga and will discuss whether these note frequencies are expected given the raga or whether it is not. 

The second part of our analysis will look at a sequence of notes taken from the clearest clip from each raga and will look at the most frequently occurring bigrams and trigrams. We will then compare these bigram and trigram frequencies with phrases that we know to be common in each raga and assess the accuracy of this quantification method. 

## Part 1: Note Frequencies
Our note frequencies for each raga were derived from the Python package librosa’s chromagram method. Given an audio time-series array, this method will assess how the pitch content of the time series is distributed over the twelve chroma bands, or pitches. 

Using a chromagram, we were able to extract which notes were played in each clip. Since a chromagram is color-coded, we extracted just the notes that were color-coded as the “loudest” in the song. In order to normalize our values and to make sure we accounted for artistic variation, we found the frequency of each note that was played for each clip. We then took the average of the frequency per note over all the clips and used that for our final note frequency value. In our visualizations, we display the top 7 most frequent notes. Ideally, these 7 notes would match exactly with the scale of every raga. We repeated this process for every raga. 

## Part 2: Bigram/Trigram Analysis
After normalizing the pitches so all of the audio clips started in C, we extracted the sequence of notes from the chromagram, following the process we used to extract notes to calculate note frequencies. Librosa’s chromagrams, however, calculate 43 notes for every 1 second of audio provided. However when analyzing a sequence of notes, unlike when analyzing note frequency in general, it was really important that we minimized any notes that were played by accident or were incorrectly picked up by librosa (noise, quite literally).  So, in order to minimize noise, we took the most-played note per second (the mode of every 43 notes). 
Once we had our sequence of notes, we removed consecutive duplicates to prevent error while calculating n-grams. This was specifically to prevent n-gram calculation from including consecutive notes because this does not provide very much information about the patterns within the raga. For example, an artist holding the note sa (C) would result in many of the most frequent bi-grams being just a note that was consecutively held. 
Calculating n-grams is useful in the scope of our project because it is very helpful in the quantification of ragas. Every raga has phrases (a sequence of notes) that form the identity of the raga. It is often after hearing one of these phrases that a listener is able to identify the raga of a song. Doing an n-gram analysis of a note sequence is a computational replication of the raga-identification method that advanced listeners use. 
 After removing these consecutive duplicates, we calculated the n-grams in our sequence of notes. Our analysis focuses mostly on the most common bigrams and trigrams found in each raga.


# Analysis: Ragas

## Raga Asavari (Hindustani) / Natabhairavi (Carnatic)
<a href="url"><img src=https://raw.githubusercontent.com/sruthiv98/RagaClassifier/gh-pages/images/Asavari2.png  align="center" height="48" width="48" ></a>
![Asavari Frequency](https://raw.githubusercontent.com/sruthiv98/RagaClassifier/gh-pages/images/Asavari2.png | width=50)
![Asavari Bi/Trigram](https://raw.githubusercontent.com/sruthiv98/RagaClassifier/gh-pages/images/Asavari1.png)
![Asavari Chromagram](https://raw.githubusercontent.com/sruthiv98/RagaClassifier/gh-pages/images/Asavari3.png)

The Asavari scale in swaras (Indian classical notes) is S R g M P d n S. In Western classical notes, in the C Major pitch, this would be C D D# F G G# A# C. As can be seen by our frequency visualization, the note that occurs with the highest frequency is G#, or the swara dha. This fits with our understanding of the raga because the main note (known as the vadi) of Asavari is dha (G#). 

Looking at the frequencies of the bigrams and trigrams, we can observe whether they match the pakad, or phrases that capture the nature of the raga. If we observe the top bigrams and trigrams, we can see the prominence of D, C, D which translates to the swaras ri, sa, ri, which is an important phrase in this raga. 


# Model 

Once these features were extracted we were able to process them into features that are usable within a model. This involved using a multi-label binarizer to one-hot encode the scales we had generated with the top 7 most frequently played/sung notes in each raga. We multiplied these one-hot encodings with the frequency with which each of these notes were played or sung. We then used these features to classify an “unseen” dataset with a Naive Bayes classifier.


# Results
We believe our results are still in the early stages, but when developed further, could be extremely impactful and applicable to the broader Indian Classical music community. Our project tackles a problem that has existed in the community for quite some time. With a model that can retain its accuracy with a wider variety of ragas, we believe that it would be an extremely useful tool for every Indian classical music listener.

After training several models using 70% of our cleaned audio data and testing with the remaining 30%, we decided to use the Naive Bayesc classifier as our final model. With this classifier, we achieved 84.2% accuracy on the test set.
