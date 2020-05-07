---
layout: page
title: Raga Classification
tagline: Quantifying and Analyzing Ragas in Indian Classical Music
description: Capstone proj
---
# Background
Indian Classical music contains two primary divisions - North Indian Classical (Hindustani), and South Indian Classical (Carnatic). While both styles have their fundamental differences, the underlying structure of styles can be captured in a raga/raag/ragam. A raga is defined as “a pattern of notes having characteristic intervals, rhythms, and embellishments, used as a basis for improvisation.” A raga can be compared to a type of scale in Western classical music. Though Western classical music does not have a direct equivalent to this concept, a raga is somewhat comparable to certain scales, such as a natural harmonic minor or a major scale. Every song has a raga that it is set to. For example, the raga Kirvani is equivalent to the natural harmonic scale in Western music.
Our goal with this project is to quantify ragas in a way that we can then build a raga identification tool. This tool would be able to “listen” to an audio clip and be able to identify the raga that the song is set to. It would mimic what seasoned listeners of Indian classical music do already: try to identify a raga while listening to music. By quantifying the features of a ragam, we will attempt to build a raga identification classifier. However, as noted by those who have attempted this in the past, “quantifying raga similarity becomes extremely challenging as it demands assimilation of both intrinsic (viz., notes, tempo) and extrinsic (viz. raga singing time, emotions conveyed) properties of ragas.” (Mishra 1) To manage the scope of this project with the time we have, we will build this tool to be functional for 10 prominent Hindustani/Carnatic ragas. These 10 prominent ragas are known as thaats. In Hindustani music, these are known as: 
- Asavari 
- Bilawal 
- Bhairav
- Bhairavi 
- Kafi 
- Kalyan 
- Khamaj 
- Marva
- Poorvi
- Todi
in Hindustani. The corresponding ragas in Carnatic are known as 
- Natabhairavi
- Dheerashankarabharanam
- Mayamalavagowlai
- Hanumatodi 
- Karaharapriya
- Kalyani
- Harikhamboji
- Gamanashama
- Kamarvardhani
- and Shubhapantuvarali.

Indian classical music has a huge number of Ragas (Carnatic alone has upward of 30,000 ragas). Given the time and resources currently available to us, it would be impossible to incorporate each of those ragas into our analysis. Thus, we are focusing on 10 major ragas, thaats. Thaats are unique because each of them have the same notes in the ascending and descending scale and are not “missing” any notes (both ascending and descending scale contain the full 7 notes). While the ragas that we picked are just a starting point, they are also important and influential ragas in and of themselves (every Hindustani raga is a derivative of one of these 10 thaats). 

Once we narrowed down which ragas we would include in our analysis, we picked songs that were set to those ragas. Since these songs came from our personal collection, which includes mostly violin and vocal music, we used almost every song that we had that was set to the appropriate raga. 
In Indian classical music, each artist plays in a specific sruthi, which is a pitch that the first note in the scale of the raga (sa) is played from. To make sure we could correctly analyze the difference between multiple songs, we identified what pitch each song was in and shifted the pitch of every song to be in C Major. We also chunked each of our songs to be 45 seconds in length so that later in our analysis, we could more accurately extract notes from them. We then loaded this information (encoded as an audio time-series array) into a csv for further use.



# Visualizaiton 1


# Visualization 2
