---
title: Final Projects
category: Syllabus
order: 1
---

# Guidance for the Final Report:

#### Due date: Saturday, May 2nd, 11:59PM 

#### Submit a pdf file electronically on Sakai 

#### Please also submit a Markdown version on Github:

> For examples of how to use markdown for your report, please find the ["Writing Papers in Markdown"](http://aiforeveryone.net/tutorials/writing_papers_in_markdown/) tutorial

-------

**Page limit:** There is a 6-page limit to the proposal (standard 12-point font, 1 in margins). Refences can go on additional pages and do not count against the limit. Be succinct but convey all necessary information. Be succinct but convey all necessary information. Conveying information effectively in a short space requires practice, so please take the opportunity to practice this important skill.

**Goal:** Final projects should be of a quality that you can show them to potential employers and use them in interviews for internships, jobs, or graduate programs. We are providing some guidance here on what would make a document good for that goal.
 
This final report should be a self-contained document that wraps up the course project. This should be a complete description of the goals and accomplishments of the project, as well as discussing whether the results are actionable. Specifically, this means whether you would actually implement this system in practice, or if the gain is minimal. Note again you will not be graded on whether the answer is yes or no, but that you have a clear discussion on the utility of the built tools. Finally, each proposal should discuss future directions on where this project should go in the future.
 
Note that it is perfectly permissive to take your own writing from the project proposal and progress report to use in this document.
 
If there was an issue raised in the feedback of the project proposal or progress report, it should be addressed in the text of the revision.
Brief Description
The goal of this status report is to get of the material for the final report together and make sure that each individual or group is on track for the final report. This involves talking about the progress so far, and the plan between now and the final report.
 
Note that it is perfectly permissive to take your own writing from the project proposal to use in this document. Furthermore, much of this document can be reused for your final report, so take care to set this up so you can reuse your work.

If there was an issue raised in the feedback of the project proposal, this must have been addressed.
 
## Expectations for a Satisfactory Final Report:

### The report should be clearly communicated
 
This progress report should be clearly written, easy to follow, and complete as a stand-alone document. Think of this as delivering a report to a customer who hired you to complete the project. Alternatively, someone who has not taken this or a similar course, but it familiar with probability/statistics and linear algebra, should be able to read your status report and conceptually understand what you have done. Beyond this, enough detail on the actual methods should be included that an expert could easily reproduce what you have done.
 
This should be a formal report. Writing, including complete sentences, grammar, etc., matters. Some important reminders:
* Don’t list the questions that need to be answered in the report, and then respond to them
* Write a stand-alone document
* Define acronyms the first time they are used (e.g. Support Vector Machine (SVM))
* Divide the report into sections and subsections to help improve the document flow
* Use a clear and descriptive title
 
### The scientific problem should be completely described.
 
You should include a description of the project and specifically include the question that you are trying to ask of the data. The document should be self-sufficient, such that someone that doesn’t have a background in that problem domain can read and understand what task you are trying to accomplish and why.
 
Provide background and context for your problem. This should be more significant than “this is a well-used prediction task from Kaggle” or something of the sort. A well-written project description will typically take at least most of a page, but there is no formal limit either high or low on what’s in here.
 
#### Some questions that a reader should be able to answer
* Why is this an interesting or important problem?
* Why is this problem significant?
* Why would this problem be interesting or significant to someone else?
* What would the potential impact of your results be?
* What is your hypothesis on the data?
* What is the relevant literature on this topic?

 
### The data should be fully described.
 
The data description should be complete and thorough. Someone reading your report should be able to achieve a good understanding of the data you are using from the written description in the report.
 
This includes details on what is the source of your data (including references if necessary), how it was collected or generated, and how this data relates to question you are trying to ask. This should also include summary statistics (e.g. number of data points, what the outcome/target distribution is, etc.).  You should utilize visualizations to help describe the data.
 
#### Some questions that a reader should be able to answer:
* What dataset is being used?
* Where did this dataset come from?
* How large is the dataset?
* What are the features of the dataset?
* What are the outcomes/labels of the dataset (if supervised)?
* How can this dataset be used to answer your scientific question?
 
### The preprocessing pipeline should be fully described.
 
The preprocessing description should include details on how the raw data was processed prior to the use of the core statistical or machine learning methodology. This can include steps such as outlier removal, data normalization, feature selection, feature extraction, etc. This should address what preprocessing steps were chosen, why those preprocessing steps were chosen, how they were implemented mathematically, and what empirical benefits the preprocessing steps convey.
 
#### Some questions that a reader should be able to answer:
* What preprocessing steps were tried?
* Why were these things helpful or necessary?
* What is the empirical support for these steps?
 
### The machine learning methodology should be fully described.
 
Include a complete description of what statistical or machine learning methodology have you chosen for this project. This description is expected to be complete and thorough and include a mathematical description of what the methodology is doing. Visualizations are often helpful to describe what the methodology is doing but depending on the method this may or may not be appropriate.

Beyond a description of the chosen methodology, illustrate why you have chosen this methodology, including a description of alternatives and discussing trade-offs evaluated when making this decision.
 
#### Some questions that a reader should be able to answer:
* What type of problem are you addressing? E.g. classification, regression, forecasting, recommendation system…
* What characteristics were key when choosing the approach?
* How does the chosen approach address these characteristics?
* How did you choose model parameters?
* How did you evaluate the performance and perform model selection? (e.g. cross- validation)
 
### The results should be succinctly and effectively communicated.
 
You should provide quantitative descriptions of how well the different system components perform (i.e. preprocessing, feature extraction, etc.). In addition to the quantitative description, you need to explain the result. Provide figures and tables to describe your results; however, do not simply present a series of figures, but talk about the interpretation and conclusions of each figure.
 
#### Some example questions that should be answered:
* Overall, how is the methodology so far doing?
* Where does the approach look promising?
* Where does the approach fall short?
* Does this solution change state-of-the-art for our given problem?
 
Figures should have captions that describe the content, and each figure should be referenced and described in the text. Use figures to help improve your explanation of your systems and potentially the results as well.

A basic checklist:<br>
- [x]  Don’t “print screen,” but export the figures to a graphics file <br>
- [x]  Label all axes<br>
- [x]  Include a legend when appropriate<br>
- [x]  Make sure that the text on the figure is large enough in the report<br>
 
You should talk about your conclusions and what future work could be done.
 
Talk about the potential impact of the results for the project, including strengths and weaknesses.

#### Some questions that should be answered:
* Where is the system satisfactory?
* What was an unexpected pitfall?
* What is the biggest area that needs improvement?
* How will your proposed work address these issues?
 
A big part of this is describing how the developed methodology could be moved from a class project to a real academic research project (i.e. future work). Note that I do not expect you to actually perform this future work. However, it is important to think critically about what would be necessary for such a task.
 
### You should use figures to convey information.
 
These expectations will be the same in the final project.
 
Figures should have captions that describe the content, and each figure should be referenced and described in the text.
 
A basic checklist:<br>
- [x] Don’t “print screen,” but export the figures to a graphics file<br>
- [x] Label all axes<br>
- [x] Include a legend when appropriate<br>
- [x] Make sure that the text on the figure is large enough in the report<br>
 
### You should include formal references.
 
These expectations will be the same in the final project.
 
Include all reference when necessary to archival material. This means published books and scientific articles, not Wikipedia. Do not cite our course notes. Succinctly, include a reference or citation for:
* Any statement or idea that is not common knowledge
* Any statement or idea that originated with someone else
* Any algorithmic approach you did not develop.

Any commonly used reference format is okay, but the style should be consistent throughout.
 
You should affirm that you adhered to the honor code in the report.
 
Should be self-explanatory.
