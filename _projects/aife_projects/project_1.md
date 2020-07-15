---
title: Predicting Mental Well-being Using Actigraphy and Sleep Data
authors: Will Wang, Karnika Singh, Peter Cho
category: AI For Everyone Projects - Spring 2020
order: 5
---

##### Will Wang, Karnika Singh, Peter Cho

### Abstract
Due to the complex nature of sleep, the task to relate sleep characteristics and human mental well-being is challenging. However, actigraphy data from wearable and portable devices has the potential to reveal this relationship. In this study, we used actigraphy data gathered by The Hispanic Community Health Study / Study of Latinos (HCHS/SOL) to predict human mental health score. Through a series of modeling techniques (logistic regression and random forest classification), we found activity has a strong influence on mental status. General mental health status can be predicted based on activity patterns (specifically percentage of time spent performing light or moderate activity while awake) and sleep behaviors (including insomnia and percentage of time during sleep period spent active) with testing accuracies varying from 62.9% to 66.5%.

### Problem Description
Sleep is critical in supporting the mental and physical well-being of human beings, but there is still much we do not know about how sleep characteristics and circadian rhythms exactly affect our health. A good night’s sleep depends not only on an individual’s length and quality of sleep but also on daily activity, sleep habits, and time spent in various sleep stages. The complex nature of sleep presents significant challenges in relating sleep characteristics to health outcomes, as it is impossible to holistically assess health based on a single visit to a sleep clinic. Actigraph data is reported to be useful in making predictions on mental well-being since activities differentially inform behavioral patterns [[1]-[6]](https://www.zotero.org/google-docs/?gJ5XdN) and [13]. Many studies have investigated similar problems, i.e., assessing the relationship between sleep and activity characteristics and psychiatric health outcomes [[2], [3], [6], [7]–[17]](https://www.zotero.org/google-docs/?C9E6F2). We hypothesize that given sleep actigraph data, it may be possible to predict rough mental health outcomes. An effective classifier would be able to discriminate between below and above average mental health status, providing potential insight into the relationship between sleep and mental wellness.

### Data Description and Preprocessing
The Hispanic Community Health Study / Study of Latinos (HCHS/SOL) [2], [10], [14] is a multi-center epidemiologic study focused on Hispanic and Latino populations. HCHS/SOL included multiple ancillary studies, including Sueño, a sleep study including a subgroup of the original cohort. The publicly available dataset contains 1,912 participants, and taken with HCHS/SOL includes continuous data gathered from polysomnograms (sleep studies which measure body functions during sleep) and wearable actigraphy (recording of activity based on physical movement), including over 1,000 mental, physical and behavioral well-being indicators. Participants of the Sueño ancillary study were given wrist actigraphy devices, Actiwatch Spectrum (Philips Respironics), to measure activity while sleeping and awake. Subjects also used the Apnea Risk Evaluation System (ARES Unicorder, Advanced Brain Imaging, Carlsbad CA) to record longitudinal physiological recordings, including airflow, respiratory effect, EEG signals, snoring intensity and patterns, head positions and movements, blood oxygen saturation, and behaviors. Summary statistics from these data inform the Apnea/Hypopnea Index, and the Insomnia Severity Index. In addition to the sleep data from Sueño, HCHS/SOL contains over 1,000 numeric values derived from surveys, medical histories, and other sources. These measures include aggregate mental health, the Hispanic stress inventory (HSI), stress from immigration, depression (from the Center for Epidemiologic Studies Depression Scale, CES-D), and the 10-Item State Trait Anxiety Inventory (STAI). For this study, only aggregate mental health scores were considered as an output. The variables included will be shown in the later sections.

### Actigraphy preprocessing
The actigraphy dataset is broken down by participants. Length and quality of actigraphy data varied between subjects. To ensure sufficient data for analysis, actigraph data was only included if there were at least 5 full days of valid data. For inclusion, such data required 6 timestamps at 00:00 AM (midnight), with no intermediate “exclude” flags. Actigraphy observations include both sleep/wake labels and activity counts per epoch of a minute. These measures are based on built-in algorithms from the actigraph device. Activity counts from actigraphy data were not standardized or normalized. Standardization was only performed immediately before modeling building and testing.

**![](https://docs.google.com/drawings/u/0/d/sTLU67qtfumKVRZqw251H1A/image?w=556&h=200&rev=5&ac=1&parent=1qnendKbl-k_8iGXfAhp8wGT6RfZtK3aCH-UKfmvfqWg)**
*Figure 1: Time Series Machine Learning Architecture*

### Label Processing
In the interest of interpretability, we elected to perform a classification task instead of regression. We focussed on the aggregate mental scores based on the SF-12 Health Survey. This subscale score is a norm-based transformation of standardized Z scores of the constituent items for the established domains. The aggregate mental score was then scaled to a mean of 50 and a standard deviation of 10. [5], [13]-[16] provide methods for interpretation and potential cutoffs for mental health status. For each age group, labels were derived based on whether a participant is above or below average based on reported mean mental health scores (stratified by age group) from [5]. This mental score reported has a confidence interval of 6.24. Participants within the average score ± 6.24 were excluded, to limit mislabeling. 910 participants meet the inclusion criteria, with 479 labelled as being in poor mental health and 491 in good mental health.

*Table 1: Features provided in the dataset*

| AGE         | Age of participant                                                                                                          | int         |
| ----------- | --------------------------------------------------------------------------------------------------------------------------- | ----------- |
| GENDER      | Gender of participant                                                                                                       | binary      |
| INCOME      | Which income group the participant belongs to                                                                               | categorical |
| SLPA36      | Apnea/Hypopnea Index                                                                                                        | numeric     |
| BMI         | Body Mass Index                                                                                                             | numeric     |
| GPAQ\_TOTAL | Total physical activity (min/day) from survey                                                                               | numeric     |
| ISI         | Insomnia Severity Index: This is a numeric variable with values ranging from 0-28 based on the Sleep Questionnaire II form. | numeric     |
| SAWA107     | Average sleep efficiency in main sleep over weekdays                                                                        | numeric     |
| SAWA108     | Standard deviation of sleep efficiency in main sleep periods over weekdays                                                  | numeric     |
| SAWA109     | Average sleep maintenance efficiency in main sleep over weekdays                                                            | numeric     |
| SAWA113     | Average wake bout in main sleep period over weekdays                                                                        | numeric     |
| SAWA111     | Average fragmentation index in main sleeps over weekdays                                                                    | numeric     |
| SAWA154     | Average sleep efficiency in main sleep over weekend                                                                         | numeric     |
| SAWA158     | Average fragmentation index in main sleep over weekend                                                                      | numeric     |
| SAWA160     | Average wake bout in main sleep period over weekend                                                                         | numeric     |
| SAWA22      | Average sleep WASO                                                                                                          | numeric     |
| SAWA24      | Sleep maintenance efficiency                                                                                                | numeric     |
| SAWA26      | Average sleep fragmentation                                                                                                 | numeric     |
| SAWA37      | Mean time in bed                                                                                                            | numeric     |
| SAWA38      | Standard deviation of the mean time in bed                                                                                  | numeric     |
| SAWA46      | Average nightly wake                                                                                                        | numeric     |
| SAWA59      | Average total time awake during in-bed periods                                                                              | numeric     |
| SAWA58      | Average snooze time in main sleep periods over all days                                                                     | numeric     |
| SAWA57      | Average wake after sleep onset in main sleep                                                                                | numeric     |
| SAWA54      | Average sleep time in main sleep period over all days                                                                       | numeric     |


*Table 2: Computed features*

| Activity Kurtosis            | Kurtosis of all activity count values for a participant                                   | numeric |
| ----------------------------- | ----------------------------------------------------------------------------------------- | ------- |
| SRI                           | Sleep regularity Index calculated based on fitting cosine curves to the sleep/wake labels | numeric |
| Sleep\_Midpoint               | Average sleep midpoint estimated based on fitting cosine curves to the sleep/wake labels  | numeric |
| Mean\_Activity                | Average of activity counts for valid epochs                                               | numeric |
| Median\_Activity              | Median value of activity counts for valid epochs                                          | numeric |
| Max\_Activity                 | Max value of activity counts for valid epochs                                             | numeric |
| Q3                            | 75 percentile activity count value                                                        | numeric |
| skew                          | Skew of the distribution of activity counts                                               | numeric |
| Std Activity                 | Standard deviation of activity counts                                                     | numeric |
| Average Total Sleep         | Total sleep epochs based on actigraphy data                                               | numeric |
| Intraday\_Activity\_Var\_STD  | Variation of the standard deviation of activity counts per day                            | numeric |
| Intraday\_Activity\_Mean\_STD | Average of the standard deviation of activity counts per day                              | numeric |

### Methods
Data were randomly split with an 80:20 ratio for the training and testing datasets. As we elected to use a classification approach, we selected several methods to predict aggregate mental status. As detailed below, we implemented logistic regression (both with and without feature subset selection), random forest regressor and support vector machine to build our classifier. Models were constructed using the training dataset, and tested on the 20% test sets. Model performance was assessed using the Receiver Operating Characteristic (ROC) Curve, which plots True Positives against False Negatives. From the ROC, the Area Under the Curve (AUC) quantifies the degree to which each model discriminates between the output classes. An AUC of 1 would imply perfect classification.
#### Logistic Regression
Logistic regression is a statistical model that uses the logistic function:


$$Pr(X_i) = {\frac{exp(\beta_0 + \beta_1X_i + \beta_2X_2 + \beta_3X_3 + \beta_4X_4 + \beta_5X_5)}{1 + exp (\beta_0 + \beta_1X_i + \beta_2X_2 + \beta_3X_3 + \beta_4X_4 + \beta_5X_5)}}$$


to predict a binary outcome variable. In logistic regression, the likelihood of the observed data is maximized by finding best coefficients $\beta_i$. In order to reduce complexity and increase interpretability, stepwise feature selection was used as well. We used AIC (Akaike Information Criteria) to minimize the stepAIC value to derive a reduced feature set. Models were tested on the held-out 20% test set, and trained on the 80% training set.

#### Random Forest
Random forest is an ensemble method of classification based on using multiple decision trees. At each tree in the forest, only a subset of the entire sample of observations was used to build the tree and at each split, only a randomly chosen subset of features (but at a fixed number) was considered. Each tree had a tunable hyperparameter related to tree size. The random forest classifier outputs predictions using the majority vote of all trees, and prevents overfitting seen in a decision tree by averaging many different trees and predictions. However, it is harder to interpret since the decision making process cannot be immediately seen. We tuned one of the hyperparameters in our model building, the number of features at each split, with cross-validation.The final model with the optimal number of features was trained, and tested on the training set using out-of-bag samples, where the predicted label of each sample was the majority vote of it’s predicted value each time it is not used in building a tree. We validated the results using testing samples separated from the training samples.

#### Support Vector Machine
Support Vector Machine (SVM) is based on maximizing the margin that best separates the observations by calculating the support vectors. Soft margins and missing classification is allowed and tuned by the parameter C for the cost of mislabelings. SVM could be a great tool for our problem as the model complexity can be tuned through choosing kernels and their hyperparameter to capture unseen structure from our dataset. Kernel tricks are always employed to better separate the observations through feature space transforms. A radial basis kernel function was used to find the optimal method for classification. The cost is a parameter that controls tradeoff between misclassification and simplicity of the model. For a low cost, a smooth decision surface is ideal while for a higher cost, more points should be classified. For RBF kernels, sigma (or gamma) which defines how far the influence of a single training example reaches is also optimized.

#### Tabular FastAI
Based on fastai library, this algorithm uses the common and established Convolutional Neural Network architecture to train on tabular data. After the network and architecture are defined, which each mini-batch of observation passes through the architecture, the algorithm performs backward propagations to minimize the loss.

#### TSAI Inception Model
The Inception Model is based on AlexNet, but specific for time series analysis. It is the state-of-the-art model for time series classification and regression analysis and we are keen to try this out on our dataset. The implementation and tutorials are provided here: [https://github.com/timeseriesAI](https://github.com/timeseriesAI). Please refer to this github page for further details. The computation is much slower. But fortunately, our dataset is pretty small and we would not need too much time to finish the computation.

#### TSAI ROCKET with Logistic Regression and Gradient Boosted Trees
From the same library and team of researchers and programmers, we found them working on a new approach. This new approach uses complex machine learning algorithms including methods based on the inception model to feature transform the time series observations. The transformed features are then used to predict the label using more traditional machine learning algorithms like logistic regression and gradient boosted trees. Logistic regression has been explained above. Gradient Boosted Trees is similar to random forest but the individual trees are added or pruned step-wise instead of all at the same time.
#### Simple Layer CNN
We also wanted to try a simple CNN implemented from a more fundamental level on our own, so that we can have more control over the specific filters we use and how we can structure the data to reflect the data’s characteristics based on domain knowledge. Here we want to reflect the inter-day regularity and restructure the dataset so that there are 1440 (minutes) per day but 5 days in total. Since there are 2 time series, each observation (one observation for one participant) has a shape of 2 by 1440 by 5. And the filters we wish to apply are all 5 by width to capture inter-day characteristics. After which we added several layers of max-pooling, dropouts and fully connected linear layers. However, at the time when this report is written, we are still debugging the details and tuning the architecture, so we do not have conclusive results for this model.

**![](https://docs.google.com/drawings/u/0/d/swug7Kko0G8uiBlfkn3h2cA/image?w=530&h=219&rev=2&ac=1&parent=1qnendKbl-k_8iGXfAhp8wGT6RfZtK3aCH-UKfmvfqWg)**
*Figure 2: CNN Architecture*

### Result
The logistic regression model achieved a training error rate of 32.73%, and a test error of 35.05%. The Percent Vigorous Activity feature was excluded by the model due to singularities. Stepwise feature selection resulted in a reduced feature set (14 features), and a test error of 37.11%. Coefficients of these models are listed in Table 1. In the logistic regression model, there is a strongly negative influence of Percent_Active_Asleep, Percent_Moderate_Activity and Percent_Light_Activity on Aggregate Mental Status. Percent_Light_Activity and Percent_Moderate_Activity remain the most influential factors in the reduced model after feature selection. These measures represent the percentage of time subjects were active while asleep, as well as the overall percentage of time with moderate or light activity.

#### Model Parameter Tuning:
1.  Random Forest: the number of trees for this classifier is fixed to be 1000. After tuning, the best number of variables at each split is 19.
2. Support Vector Machine: After tuning, a support vector machine classifier is found to have the best performance with the parameters: gamma = 0.0156, cost = 2, kernel = radial basis function.

The Random Forest classifier with 1000 trees gave a similar performance to logistic regression in terms of error rate, but comparatively overfit on positive labels and underfit on negative labels. The most important variables included ISI, income group, SAWA108 (standard deviation of sleep efficiency), sleep midpoint, and SLPA36 (apnea index). Notably, the features most relevant to the random forest classifier differ from those selected by the stepwise subset selection.
**![](https://lh4.googleusercontent.com/hKSm8s1vthKT3bWvCampzENEgMyWX25e4FduUVVUNF3pDfzlmch10OlmqtfTnwkMsd6m8FT6Z9PCJHRa5IWcLdLyhbZy3KEw_yx814l4ZrQDkuVMVQl2_DtXpNQpdJYnmZvWKGeI-ty6Rg)**
*Figure 3: Variable importance of a tuned random forest classifier*


*Table 3: Classical Machine Learning Model Summary*

| Model                                               | Training Accuracy | Testing Accuracy | F1-Score | AUC    |
| --------------------------------------------------- | ----------------- | ---------------- | -------- | ------ |
| Logistic Regression                                 | 67.27%            | 64.95%           | 0.66     | 0.682  |
| Logistic Regression with Stepwise Feature Selection | 68.56%            | 62.89%           | 0.64     | 0.663  |
| Random Forest                                       | 63.66%            | 66.49%           | 0.6860   | 0.666  |
| Support Vector Machine with RBF Kernel              | 63.66%            | 63.40%           | 0.6758   | 0.6926 |


The four models that we built and tested all have comparable performance. The strong contribution of activity during sleep periods to a lower than average aggregate mental status is promising for our hypothesis. Comparing the ROC curves for each model, we find that the SVM performed best (AUC=0.6926), closely followed by logistic regression (AUC=0.682) without subset selection. Unfortunately, none of the SAWA measures had high contributions in the logistic regression models, implying the possibility that there is no direct contribution from measures related to sleep efficiency or duration on mental health outcomes. However, the random forest model gives a different set of important variables from stepwise feature search. There may be more complex interactions going on between variables across this dataset that aren’t adequately captured by any single method implemented here.

**![](https://docs.google.com/drawings/u/0/d/sQqa_0tU-Kl_LVHI-h_wGsg/image?w=433&h=388&rev=20&ac=1&parent=1qnendKbl-k_8iGXfAhp8wGT6RfZtK3aCH-UKfmvfqWg)**
*Figure 4: Receiver Operating Characteristic Curve for each model. Area Under the Curve: Logistic Regression = 0.682, Stepwise Selection = 0.663, Random Forest = 0.666, SVM = 0.6926.*

*Table 4:  Deep Learning Model Summary* 

| Method/Library                          | Testing Accuracy |
| --------------------------------------- | ---------------- |
| FastAI Tabular                          | 66.5%            |
| TSAI Inception                          | 65.6%            |
| TSAI ROCKET with Logistic Regression    | 51.5%            |
| TSAI ROCKET with Gradient Boosted Trees | 53.5%            |


### Conclusions and Future Work 
Through careful data preprocessing and then building and validating our predictive models, we were able to build and test multiple classification algorithms that predict a general status of mental well-being based on activity patterns and sleep behaviors. The model test accuracies range from 62.9% to 66.5%, for a dataset with a 46:54 label split. These models indicate that there are trends and patterns to discover in this problem, but our models have subpar performances. One interesting observation is that the most state-of-the-art time series machine learning model, the Inception Model on only actigraphy data, is able to rival the performance of a model with carefully constructed features as well as additional demographics and survey scores. This is heartening for a problem with no exactly similar prior work, and especially for a problem with regards to mental health. We believeThe pitfalls of this project are that we have not exhausted all potential classification methods, and that we have not fine tuned every hyperparameter in more complex models, the Inception Model, Random Forest and ROCKET approaches. Interestingly, the most recently developed approach, the ROCKET method, does not perform as weli.e. Random Forest. We will in turn try Support Vector Machines with radial bl as the Inception Model or even the simplest logistic regression model, suggesting that this approach still needs further investigation and fine-tunThe pitfalls of this project are that we have not exhausted all potential classification methods, and that we have not fine tuned every hyperparameter in more complexing. Another way to find a better predictive models, i.e. Random Forest. We will in turn try Support Vector Machines with radial basis function kernel, Adaboost, and Gradient Boosted Trees while searching through the entire grid of potential hyperparameter domaingsl asin.s to use a much larger dataset for another problem and use transfer learning to adapt to this specific problem.

### References

[1] N. Pop-Jordanova, S. Markovska-Simoska, M. Milovanovic, and D. Lecic-Tosevski, “Analysis of EEG Characteristics and Coherence in Patients Diagnosed as Borderline Personality,” PRILOZI, vol. 40, no. 3, pp. 57–68, Dec. 2019, doi: [10.2478/prilozi-2020-0005](https://doi.org/10.2478/prilozi-2020-0005).

[2] E. M. Cespedes et al., “Comparison of Self-Reported Sleep Duration With Actigraphy: Results From the Hispanic Community Health Study/Study of Latinos Sueño Ancillary Study,” Am. J. Epidemiol., vol. 183, no. 6, pp. 561–573, Mar. 2016, doi: [10.1093/aje/kwv251](https://doi.org/10.1093/aje/kwv251).

[3] G. L. Bullock and U. Schall, “Dyssomnia in Children Diagnosed with Attention Deficit Hyperactivity Disorder: A Critical Review,” p. 5, 2005.

[4] T. R. Seech, M. E. Funke, R. F. Sharp, G. A. Light, and K. J. Blacker, “Impaired Sensory Processing During Low-Oxygen Exposure: A Noninvasive Approach to Detecting Changes in Cognitive States,” Front. Psychiatry, vol. 11, p. 12, Jan. 2020, doi: [10.3389/fpsyt.2020.00012](https://doi.org/10.3389/fpsyt.2020.00012).

[5] 2001 Utah Health Status Survey, Utah Department of Health, “Interpreting the SF-12.” [Online]. Available: [http://health.utah.gov/opha/publications/2001hss/sf12/SF12_Interpreting.pdf](http://health.utah.gov/opha/publications/2001hss/sf12/SF12_Interpreting.pdf).

[6] L. Sequeira et al., “Mobile and wearable technology for monitoring depressive symptoms in children and adolescents: A scoping review,” Journal of Affective Disorders, vol. 265, pp. 314–324, Mar. 2020, doi: [10.1016/j.jad.2019.11.156](https://doi.org/10.1016/j.jad.2019.11.156).

[7] A. Bluschke, M. L. Schreiter, J. Friedrich, N. Adelhöfer, V. Roessner, and C. Beste, “Neurofeedback trains a superordinate system relevant for seemingly opposing behavioral control deficits depending on ADHD subtype,” Dev Sci, p. desc.12956, Feb. 2020, doi: [10.1111/desc.12956](https://doi.org/10.1111/desc.12956).

[8] A. E. Hanish, D. C. Lin-Dyken, and J. C. Han, “PROMIS Sleep Disturbance and Sleep-Related Impairment in Adolescents: Examining Psychometrics Using Self-Report and Actigraphy,” Nursing Research, vol. 66, no. 3, pp. 246–251, 2017, doi: [10.1097/NNR.0000000000000217](https://doi.org/10.1097/NNR.0000000000000217).

[9] D. Koshiyama et al., “Resting-state EEG beta band power predicts quality of life outcomes in patients with depressive disorders: A longitudinal investigation,” Journal of Affective Disorders, vol. 265, pp. 416–422, Mar. 2020, doi: [10.1016/j.jad.2020.01.030](https://doi.org/10.1016/j.jad.2020.01.030).

[10] R. Mueller, “Sleep Data - National Sleep Research Resource - NSRR.” [https://sleepdata.org/](https://sleepdata.org/) (accessed Mar. 02, 2020).

[11] S. Baddam, C. Canapari, S. van Noordt, and M. Crowley, “Sleep Disturbances in Child and Adolescent Mental Health Disorders: A Review of the Variability of Objective Sleep Markers,” Medical Sciences, vol. 6, no. 2, p. 46, Jun. 2018, doi: [10.3390/medsci6020046](https://doi.org/10.3390/medsci6020046).

[12] N. L. Johnson et al., “Sleep Estimation Using Wrist Actigraphy in Adolescents With and Without Sleep Disordered Breathing: A Comparison of Three Data Modes,” Sleep, vol. 30, no. 7, pp. 899–905, Jul. 2007, doi: [10.1093/sleep/30.7.899](https://doi.org/10.1093/sleep/30.7.899).

[13] S. Miano, M. Esposito, G. Foderaro, G. P. Ramelli, V. Pezzoli, and M. Manconi,“Sleep-Related Disorders in Children with Attention-Deficit Hyperactivity Disorder: Preliminary Results of a Full Sleep Assessment Study,” CNS Neurosci Ther, vol. 22, no. 11, pp. 906–914, Nov. 2016, doi: [10.1111/cns.12573](https://doi.org/10.1111/cns.12573).

[14] C. Alcántara et al., “Stress and sleep: Results from the Hispanic Community Health Study/Study of Latinos Sociocultural Ancillary Study,” SSM - Population Health, vol. 3, pp. 713–721, Dec. 2017, doi: [10.1016/j.ssmph.2017.08.004](https://doi.org/10.1016/j.ssmph.2017.08.004).

[15] G. Vilagut et al., “The Mental Component of the Short-Form 12 Health Survey (SF-12) as a Measure of Depressive Disorders in the General Population: Results with Three Alternative Scoring Methods,” Value in Health, vol. 16, no. 4, pp. 564–573, Jun. 2013, doi: [10.1016/j.jval.2013.01.006](https://doi.org/10.1016/j.jval.2013.01.006).

[16] “Vilagut et al. - 2013 - The Mental Component of the Short-Form 12 Health S.pdf.” .

[17] M. T. Smith et al., “Use of Actigraphy for the Evaluation of Sleep Disorders and Circadian Rhythm Sleep-Wake Disorders: An American Academy of Sleep Medicine Clinical Practice Guideline,” Journal of Clinical Sleep Medicine, vol. 14, no. 07, pp. 1231–1237, Jul. 2018, doi: [10.5664/jcsm.7230](https://doi.org/10.5664/jcsm.7230).
