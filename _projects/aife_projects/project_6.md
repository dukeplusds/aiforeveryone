---
title: Applying 1D CNN to Commercial EEG Data to Determine Attention State
authors: Ben Shepard, Virginia Patterson, Nicole Schewartz, Scott Lu, Yuze Zeng
category: AI For Everyone Projects - Spring 2020
order: 6
---

Ben Shepard, Virginia Patterson, Nicole Schewartz, Scott Lu, Yuze Zeng

### Background
The ability to measure brain waves - electrical signals produced by the firing of neurons in a brain - has been possible for over half a century. Electroencephalography (EEG), a relatively new technology, is a non-invasive method of measuring electrical signals through the scalp. Unfortunately the technology has been limited to those medical and research laboratories with enough funding to purchase tens of thousands of dollars worth of necessary equipment. Recently, simplified consumer EEG devices have entered the market in the form of portable wearables. These relatively inexpensive devices, some which claim to be “research-grade,”  leverage EEG technology to monitor your mental activity in order to assist in focus-training, meditation, and stress management. 
In addition to the promised personal benefits, access to inexpensive, accurate, and consistent neurofeedback would provide substantial research opportunity. However, the benefits of these wearable devices are not without their disadvantages. Their limited number of sensors and fixed positioning on rigid frames combined with use in sub-optimal environments that are prone to signal noise bring into question the usefulness of any data gathered.
The urgency around looking at the data from consumer EEG devices revolves around its vast potential to benefit people and industries. Truck drivers could be alerted when there are early warning signs they are tired and should pull over, children with ADD could learn early on under what conditions and how they concentrate better, athletes may be able to perform better, understanding when they are losing their full focus. These are just a few examples. EEG technology is specialized, expensive, and exclusive, while these consumer models come as low as $200, are very portable and can plug into one’s phone to gather information. Making such a technology so accessible positively impacts medical research, neurological research, and reaches various different audiences. 
Developing machine learning models for interpreting consumer EEG-generated data could assist in highlighting their strengths and weaknesses, validating or refuting the manufacturers claims, and in interpreting results on the potentially large pools of consumer and researcher data that could become available through their widespread use.

### Literature Discussion
The focus of our project is based on a 2019 study by Aci, C.I. et. al. (2019), that  determined a novel approach to assessing and training models of varying attention states based on minimal to no outside distractions. The study is focused on three states of mental activity: 1) Focused passive attention, 2) Detached but awake, 3) Drowsy and unfocused.  Each state was performed within a 10 minute time span for a duration of approximately 35 - 55  minutes per participant for 7 days.    
There are four categories of brainwaves ranging from the most activity to the least activity: beta, alpha, theta, delta. Beta waves are the fastest, occur when the brain is actively engaged in mental activity, have a low amplitude. Their frequency ranges from 15 to 40 cycles per second (CPS) and are characteristic of a strongly engaged mind [5]. 
Alpha brainwaves indicate non-arousal, are slower and higher in amplitude, with a frequency range from 9 to 14 CPS. Examples of alpha states include sitting down to rest after completing a task, taking time out to reflect or meditate, or taking a break outside after a meeting [5].
Theta waves possess an even greater amplitude and slower frequency, with a  range between 5 and 8 CPS. Examples include daydreaming after a task or driving on a freeway unable to recall the last five miles.  Activities that are repetitious in nature with minimal differentiations or distractions can induce a theta state.  Tasks become automatic such that one mentally disengages from them. Free flow ideation without guilt or censorship can take place, and it is often a very positive mental state.  [5].
Lastly, delta waves  have the greatest amplitude and slowest frequency and typically have a range of 1.5 to 4 CPS, indicating drowsiness to a deep dreamless sleep at the lowest frequencies [5]. 
According to the Aci, C.I. et. al. study (2019), the number of focused and unfocused attention states are associated with enhanced or suppressed EEG activity at 1–10 Hz frequency bands in the frontal EEG channels F3, F4, and Fz. Alternatively, the drowsing state is observed as continuous or intermittent power spouts at alpha-band frequency in the EEG signals at 10–15Hz and the EEG channels C3, C4, Cz, and Pz.  This will be considered as data extraction and labeling continue.

### Scientific Question
Our project attempted to answer whether we can train a model that detects loss of attention from data gathered from commercial EEG data? Monotonous tasks often prompt fatigue or sleepiness; is there a way we could train a model so that workers, who perform these tasks, could be alerted to take a break and rest during these moments, using a consumer EEG headset?

### Preprocessing pipeline: Wroking with the Data
The Kaggle dataset “EEG Data for Mental Attention State Detection” [1] was used to train the proposed model. This data was gathered using a consumer grade EEG Emotiv headset. Described in the paper by Cigdem Inan Aci[2], this data set is taken by having participants experience 3 different levels of focus while playing through a train simulator. The EEG data of each participant was recorded for 3 10-minute intervals, each phase corresponding to: 1) Focused passive attention, 2) Detached but awake, 3) Drowsy and unfocused. There were a total of 34 participant data in our dataset, each with 25 columns, 14 of which looked at first to be EEG data. The researchers then used Support Vector Machine (SVM) to identify the characteristics of the states with the EEG data.
The original mat file provided timestamps for which the change in phase occurred. These timestamps were used to label the sections of the data, where the previously described phases are labeled from 1 to 3 correspondingly. 
The Kaggle data was in Matlab originally, in a single struct. We prepared the data by extracting the time series generated by the EEG devices and converted the timestamps. It was  trimmed, the corresponding labels were extracted and placed in the data matrix, and it was converted into a CSV. Our group came across some limitations in terms of the way these Emotiv headsets work, and their channels. The data only had high levels of frequency for each sensor. Each sensor gathers 5 bands of EEG information. The relationship with theta and beta waves could have helped understanding correlations and the hemispheres for various states of attention. 
We labeled the data in order to reduce excess channels and trimmed it down to isolate the specific channels EDF4 and EDF5. [See Figure 3]
![](https://i.imgur.com/oVfHpsJ.png)
Figure 2: [1.0] focused, [2.0] unfocused, [3.0] drowsy, Data Batches with only E and O channels

**EEG Specific Data**
The authors of the study used a modiﬁed Epoc EEG head providing 12 channels real-time EEG data at a sampling rate of 128 Hz, a voltage resolution of 0.51 μV, and a bandwidth between 0.2–43 Hz.  The nodes were modified such that the electrodes were placed over frontal and parietal lobes of the scalp. 
The positions of the electrodes used in this work were F3-Fz-F4-C3-Cz- C4-T3-T4-T5-T6-Pz in a standard 10–20 system. Four leads are identiﬁed by the locations T3, T4, T5, and T6 were used to supply current and establish the EEG reference, therefore those data points are not viable. Most importantly, the acquired data from the 7 leads were identiﬁed by F3, F4, Fz, C3, C4, Cz, and Pz. This is important to note as we read, extract, and select data for our model.

### Methodologies and Models
Recently, convolutional neural network (CNN) is found to be particularly useful in classifying one-dimensional (1D) signals for time-series data like EEG [3]. It can learn multiple filters that are used to convolve with small portions of input data (i.e., convolution) to extract time-invariant features. It has demonstrated a superior performance when dealing with limited labeled data and high signal variations acquired from different sources. When compared to 2D CNN commonly used for images and videos, 1D CNN has several advantages: (1) forward propagation and backpropagation only require array operations instead of matrix operations; (2) a small number of hidden layers or shallow architecture is needed; (3) computational requirements are low [4].  
The configuration of a 1D CNN involves several hyper-parameters (Figure 1): (1) number of hidden CNN and multilayer perceptron (MLP) layers; (2) filter size in each layer; (3) subsampling factor in each layer; (4) choice of pooling and activation functions [4].
![](https://i.imgur.com/Lo9pwNG.png)
Figure 3: A sample configuration of 1D CNN [4]

We tried three different learning models:
1. Fastai.column_data (fastai v0.7)
2. Fastai.tabular (tabular_learner)
3. Faistai2 - Time Series AI (tsai)

Fastai v0.7 failed. Tabular_learner was easy in implementation but, ultimately, provided an insufficient visualization for time series EEG. Additionally, it lacked the ability to generalize among the tabular files as each contained around 400,000 time points. Tsai provided a good visualization; however, required additional data cleaning and formatting. Data needed to be in a 3d array with a certain format. We finalized on Fastai2 even though it was difficult to tell the features associated with each state. The results were less than successful as we discerned the limitation of feature engineering. Feature engineering of data is critical using Fourier transferral and identification of key channels in their placements. [Figure 4]
![figure 4](https://i.imgur.com/8cj1EzD.png)
Figure 4: A diagram representation feature engineering

### Conclusions and Discussion:
 Ultimately, our model performed poorly and we were unable use our 1D CNN to identify various attention states. We realized that feature engineering of EEG data is critical, as said above, along with a subject-specific and accurate dataset. In general the preprocessing pipeline exposed a lot of issues to our group that we did not anticipate. 

With an increasing rise in the diagnosis of psychological, attention, and mood disorders, being able to determine mental state and levels of consciousness at various time intervals and under certain conditions in an automated way is valuable. Commercial EEG devices, if reliable, will greatly increase the data available. Training a model to do the work that doctors have to do in testing might not only be more efficient, but more accurate as well. While our work was unsuccessful, the impact for the process of this work takes steps in a larger effort to use machine learning to label brainwave data and further understand levels of consciousness and various neurological states. 

### References:
[1] https://www.kaggle.com/inancigdem/eeg-data-for-mental-attention-state-detection

[2] https://www.sciencedirect.com/science/article/pii/S0957417419303926

[3] Supratak, Akara, et al. "DeepSleepNet: a model for automatic sleep stage scoring based on raw single-channel EEG." IEEE Transactions on Neural Systems and Rehabilitation Engineering 25.11 (2017): 1998-2008.

[4] Kiranyaz, Serkan, et al. "1D convolutional neural networks and applications: A survey." arXiv preprint arXiv:1905.03554 (2019).

[5] Herrmann, N. “What is the function of various brainwaves.” Scientific American.(1997).  
    Sourced from: https://www.scientificamerican.com/article/what-is-the-function-of-t-1997-12-22/


