---
title: Detecting Misinformation and Unreliability in News Articles
category: +DS Advanced Projects - Spring 2020
authors: Cindy Weng
order: 3
---

## Introduction

Misinformation is defined as:
> **false or inaccurate information, especially that which is deliberately intended to deceive.**

Misinformation has become increasingly prevalent in all forms of media and its presence has made a significant impact on society. It degrades society’s trust in news outlets and amplifies alternative narratives, distorting the truth and causing discrimination, prejudice, other social issues.

The recent coronavirus crisis has made apparent the importance of delivering accurate and reliable news, as well as how misinformation has had serious implications.


We can help reduce misinformation by providing users with quantitative information on how accurate an article is; automating this process can make it more efficient and widespread.

## Data
The data consisted of a collection of news articles with its respective author name, the text of the article, and a binary label on whether or not the article is reliable. The entire dataset had 20,000 observations, but due to some running time limitations, only a subset of these observations were used.

An excerpt of an article that's classified as 'reliable':
> A Caddo Nation tribal leader has just been freed after spending two days behind bars in North Dakota. Family members say she was simply an innocent bystander in a clash between police and protesters, and was not guilty of anything the police claimed. 

An excerpt of an article that's classified as 'unreliable':
>While the Obama Administration has made much of its intention to start a full-scale cyberwar against Russia. the most recent reports suggest that the war is effectively on hold at least until the presidential election in two weeks. From President Obama‚ the hope is to work with Hillary Clinton, if she becomes president-elect, to launch a cyber war that they both can get behind. Indeed, both have appeared very hawkish against Russia, and Obama apparently doesn’t want to deny Clinton a chance to participate in the early days of a war she’d inherit. 

Sometimes, we can tell when an article has malicious intents or is intentionally trying to decisive us, but other times, this can be very subtle and go unnoticed, which is where natural language processing can help us. 

## Text classification

One goal of this project is to be able to label a given article as either 'reliable' or 'unreliable', provided the text of the article. Several approaches were taken to accomplish this, but it was found that using transformers was the most accurate method.

### Sentiment analysis

One possibility that was considered was to use sentiment analysis on the article text. However, sentiment analysis is largely only effective on short segments of text, not large bodies, as the sentiment of a lengthy article could fluctuate at different points. 

We considered using sentiment analysis on the title, but across the entire data set, 35.7% of the titles of 'unreliable' articles were classified as positive and 38.3% of the titles of 'reliable' articles were classified as positive. Since the proportions of articles with positive and negative tones are relatively similar between 'reliable' and 'unreliable' articles, sentiment analysis would not be suitable for this data set.

Based on these results, we've decided that sentiment analysis alone is not a complex enough classification method for classifying 'reliable' vs. 'unreliable' articles; the differences of the text between these two labels have much more nuance than sentiment analysis is capable of capturing.

### Naive Bayes classifier

Another attempt at classification was made using a Naive Bayes classifier. It relies on the use of a term document matrix (a list of word frequencies for the articles). Once we have made the TDM, we apply Bayes' rule. 

Given that we've seen **X**, where **X** is a  vector containing the words coming from either an unreliable or reliable article, we calculate the probability that the article that we took the vector of words from is reliable or unreliable. We then take the maximum between the two probabilities (the probability that the article is 'reliable' given that we've seen **X** or the probability that the article is 'unreliable' given that we've seen **X**) to determine the final classification.

This attempt was relatively successful with 94% accuracy. However, despite the Naive Bayes classifier's relatively high accuracy, one reason that we believe transformers (discussed in the next section) will be a more robust classifier is because the Naive Bayes classifier is too reliant on the TDM. 

Sometimes, just using the frequencies of words in a document is not enough; in order to be thorough, we need to be able to consider other details, the context in which these words are being used or the positioning of these words relative to each other. Transformers will be able to provide us with this robustness.

### Transformers

Transformers are a type of machine learning model used that can be used for different types of natural language processing tasks; here, we use it for classification. 

Transformers have been heavily pre-trained for general NLP tasks and can be fine tuned for more downstream tasks, such as the one we have at hand. Originally, recurrent neural networks (RNNs) and long-short term memory (LSTM) architecture were other models that were also considered for the task. However, RNNs do not fare well when it comes to long-term dependencies in lengthier bodies of text; LSTMs are a slight improvement upon this, but still have similar problems. 

RNNs and LSTMs read input sequentially, which limits both their ability to parallelize during training and their ability to contextualize words. Transformers can read the entire input at once, allowing them to capture the context of the text more holistically and accurately and to train with parallelization. 

We trained three types of transformers, BERT, RoBERTa, and DistilBERT, over eight epochs and then tested them. RoBERTa and DistilBERT are variations of the BERT model.

Using a samples of 800 observations, BERT achieved an accuracy of 97.5%, RoBERTa achieved an accuracy of 98.8%, and DistilBERT achieved an accuracy of 98.1%. Out of the attempted methods of text classification, transformers have yielded the best accuracies. In the future, we hope to be able to increase the sample training size, as the running time environment limited the training set size.


## Text generation

We use the generative transformer, GPT-2, to perform natural language generation.

Given data, the model will output text that is similar in style or content. Below are examples of text generated from reliable articles; they appear fairly realistic and natural. We chose to generate text from articles labeled as ‘reliable’ because text generation can often be used for malicious purposes such as spreading misinformation, and even if an article is generated from reliable articles, it does not necessarily mean it will contain reliable or factual information. In this case, the sum of the parts does not equal the whole. 

### An excerpt from a sample of generated text:
>Fifty years later, I finally found a way to look back at those years and tell the story of how I got involved in and off the West Side of Chicago, an amazing, successful neighborhood in the heart of the South. It was the winter of 1965, and we were living next door on the corner of South Park Boulevard between Central and North, on South West. By the time we dropped off for a few years, I was almost 50 years old, so I was wearing my old, leathery suit like the kid from the movies: smooth and white, with a plumper overcoat and sneakers— a classic West Side kid, as I put it, so cool. We had been living on the Lower West Side for six years. And this is the first time I had seen the neighborhood since I was a child [in the 1950s]. I wasn’t really an outsider. I wasn’t actually an outsider, either.  In the   months of the 1960s, the city had been expanding rapidly. The streets were mostly empty. There were buses everywhere. One guy was driving the bus, and the other was a guy driving, but he had to turn out to be a cab driver, so I had to take him in one for the night, and then I had to go home. So one night I was on my own, and two guys were sitting at the bar, and I said, “You’re coming back. ” Why would I do this? It’s my destiny. 

### An excerpt from another sample of generated text:
>LONDON  —   A police sniper killed 17 people at Heathrow Airport on Monday, just days after England’s   vote that helped elect a new Conservative prime minister. The shooting at the gate of Terminal 2 of the World Trade Center came three days after the British government condemned the vote and said that Britain’s departure from the European Union would destabilize the United Kingdom’s economy “with a sharp increase in the threat of terrorism,” the Guardian reported. As a result, the United Kingdom will now be forced to quit the union, Britain’s foreign affairs minister, Boris Johnson said. As of late Thursday evening, the exit vote had largely been suspended while the federal Conservatives, led by Theresa May, sought “a return to the normalcy and security of the European Union,” and Prime Minister John Key said he was “convinced” a new European deal for freedom of movement in Britain would be agreed early in the process, the BBC reported. “We want an orderly process,” Mr. Johnson told reporters in London on Tuesday, according to Radio Times. “We are also convinced that the British people will make a choice on whether or not to remain in the E.U.”

I noticed the bottom article mentioned the Heathrow airport - what’s interesting is that when looking through the complete dataset of reliable articles, only one of the ~10 articles mentioning Heathrow airport was about terrorism (the others were about racial profiling, airport renovations, and other topics); this article that mentioned Heathrow airport discussed the Manchester attacks, not a police sniper killing. I also looked around the dataset to see where BERT got the '17 people' statistics from, and other articles in the dataset that mentioned '17 people' had to do with deaths from hurricanes, deaths in Germany from a terrorist attack, or injuries in Hong Kong from a subway incident. Doing this fact-checking leads us to conclude that the generated text is not necessarily factual; in this case, it often just pieces together random facts from various articles to appear factual. 

### Classifying generated text

We've established that generated text is often not reliable or accurate, even if it is generated from reliable news articles. However, BERT classified these generated texts as 'reliable', which can be problematic. This could potentially be resolved by training BERT to distinguish between generated and non-generated text in addition to classifying whether or not a given text is reliable. Classification was only done on a few samples of generated text, but further experimentation can be carried out to find more detailed problems and solutions.

Fact-checking this generated text can be time-consuming (here, I’ve only fact checked a few generated texts so far) and is another issue to tackle, but gives us insight on the consequences of the accessibility of text generation models like this and how easily people can use it to spread misinformation, as these models are very adept at mimicking language patterns.

## Future work

In the future, we hope to use multilevel classification rather than binary classification when determining the reliability of a news article. Classifying text on a spectrum could provide people more information when deciding how much trust to place in an article.

Another topic we hope to explore is integrating additional article information, such as the news company that produced the article, the title of the article, and the author of the article, when training the transformers for text classification. These additional features could provide more valuable insight on what makes a news article reliable or not.