# Cross Synchrony Entropy (tentative name)
NOTE: Examples are still in progress. However, the code is available for user to test it out. Within the **synchro_code** folder, it contains the codes for **Cross Synchrony Entropy** and **Global Field Synchronization**

**Contact**: choonghengjie@yahoo.com

Alternative method to quantify the synchrony of the system through information geometry.

Here, I would like to introduce an alternative method for quantifying the synchrony of a system using signals known as **Cross Synchrony Entropy (CSE)**. Typically, the synchrony of a system is assessed through **Global Field Synchronization (GFS)**, which can quantify synchrony at specific frequency. However, GFS may not perform optimally when applied across a range of frequencies, such as EEG alpha bands (8-16Hz). This is because it requires averaging GFS values across all frequencies within the band, leading to varying average values depending on the interval of interest during evaluation. A higher frequency interval (e.g., 1Hz) may not provide an accurate representation of the desired frequency range, while a lower frequency interval (e.g., 0.1Hz) would increase computation time.

To address this issue, I evaluate synchrony through the phase difference between signals within an interested frequency range. This is accomplished by assessing the angle difference between the analytic signals (e.g., $\Delta \theta$), which are complex-number signals obtained through the Hilbert transform. The angle difference is then evaluated using the **cosine** function (e.g., $`\cos(\Delta \theta)`$) to constrain the phase difference to a range of -1 to 1. Here, a value of 1 indicates that the signals are oscillating in phase, while a value of 0 signifies a 90-degree phase shift. This evaluation is performed for each time point between the given signals, resulting in a series of phase difference matrices known as the **phase-lock matrix**. It should be noted that the phase-lock matrix is symmetric. To assess the synchronicity of the system, the upper triangle of the phase-lock matrices is collected to form a probability distribution ranging from -1.5 to 1.5 (ideally 1.0, but the reference distribution may not be perfectly represented). This distribution is then compared with a **reference distribution (a normal distribution)** with a mean of one and a standard deviation of 0.1 (which users can choose to adjust). This choice of reference distribution allows for a small tolerance for discrepancies caused by noise. To compare the system distribution with the reference distribution, the **Wasserstein distance** is utilized, as it quantifies the minimum cost required for one distribution to match another distribution.

NOTE: the written function also includes other metric like **hellinger distance** and **Jensen Shannon divergence** alongside **wasserstein distance**. 

NOTE: Shannon entropy is not used because same value would be expected for system that **total/constant out of phase at 90 degree** and **total/constant in phase**. 


Interested reader may refer to the following reference(s):
1. Decreased functional connectivity of EEG theta-frequency activity in first-episode, neuroleptic-naive patients with schizophrenia: preliminary results
2. Cognitive performance in healthy older adults relates to spontaneous switching between states of functional connectivity during rest

# Requirements
* numpy
* scipy
* sklearn 
* joblib
* tqdm
