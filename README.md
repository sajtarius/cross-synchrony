# Cross Synchrony Entropy (tentative name)
NOTE: Examples are still in progress. However, the code is available for user to test it out. Within the **synchro_code** folder, it contains the codes for **Cross Synchrony Entropy** and **Global Field Synchronization**

**Contact**: choonghengjie@yahoo.com

Alternative method to quantify the synchrony of the system through information geometry.

Here, I would like to show an alternative method to quantify the synchrony of a system through signals known as **Cross Synchrony Entropy (CSE)**. In general, the synchrony of a system can be quantified by **Global Field Synchronization (GFS)** which able to quantify the synchrony of the system at a specific frequency. Hence, it may not work well when utilizing it to a range of frequency (e.g. EEG alpha bands (8-16Hz)). This is because one needs average the GFS after evaluate the GFS for all the frequencies within the frequency band which the average value would vary depending on the interested interval when evaluating GFS. Higher frequency interval (e.g. 1Hz) would not able to get a proper GFS of the interested frequency range. On the other hand, lower frequency intervel (e.g. 0.1Hz) would subsequently increase the computation time. 

To overcome the state problem, here I evaluate the synchrony through the phase difference between the signals at a interested frequency range. This can be achieved by evaluating the angle different between the analytic signals (e.g. $`\Delta \theta`$). The analytic signal is a series of complex number signal which can be obtained after going through Hilbert transform. The angle different is evaluated with **cosine** (e.g. $`cos(\Delta \theta)`$) to limit the range of phase different to -1 to 1; it is trivial that 1 would signify that the signals are oscillating in phase, while 0 is 90 degree out of phase. This evaluation can be done between the given signals at every time points. Subsequently, a series of phase different matrices (known as **phase lock matrix**) is expected. It is trivial that the phase lock matrix is a symmetric. Hence, to evaluate the synchronicity of the system, the upper triangle of the phase lock matrices are collected to form a probability distribution that ranging from -1.5 to 1.5 (ideally would be 1.0, but reference distribution would not be well represented) and compared with **reference distribution (normal distribution)** that has the mean of **one** and standard deviation of **0.1** (user can choose to increase it) since fully synchronized system would have the cosine of the phase different of ONE. The normal distribution is used as a reference distribution to allow small discrepency tolerance (e.g. small standard deviation of 0.1) that may be caused by the noise. In term of comparing the **system distribution** and **reference distribution**, wasserstein distance is used since it quantify the minimum cost required for one distribution to achieve another distribution. 

NOTE: the written function also includes other metric like **hellinger distance** and **Jensen Shannon divergence** alongside **wasserstein distance**. 

NOTE: Shannon entropy is not used because same value would be expected for system that **total/constant out of phase at 90 degree** and **total/constant in phase**. 


Interested reader may refer to the following reference(s):
1. Decreased functional connectivity of EEG theta-frequency activity in first-episode, neuroleptic-naive patients with schizophrenia: preliminary results
2. Cognitive performance in healthy older adults relates to spontaneous switching between states of functional connectivity during rest

# Requirements
* Numpy
* Scipy
* sklearn 
* Joblib
* tqdm
