# Text-Summarization-using-Transformers-T5


### Introduction

we will  fine tuning a transformer model for **Summarization Task**. 
In this task a summary of a given article/document is generated when passed through a network. There are 2 types of summary generation mechanisms:

1. ***Extractive Summary:*** the network calculates the most important sentences from the article and gets them together to provide the most meaningful information from the article.
2. ***Abstractive Summary***: The network creates new sentences to encapsulate maximum gist of the article and generates that as output. The sentences in the summary may or may not be contained in the article. 

we will be generating ***Abstractive Summary***. 


* We will be using : [Weights and Biases Service](https://www.wandb.com/) WandB in short.
* It is a experiment tracking, parameter optimization and artifact management service. That can be very easily integrated to any of the Deep learning or Machine learning frameworks. 

The notebook will be divided into separate sections to provide a organized walk through for the process used. This process can be modified for individual use cases. The sections are:

1. [Preparing Environment and Importing Libraries](#section01)
2. [Preparing the Dataset for data processing: Class](#section02)
3. [Fine Tuning the Model: Function](#section03)
4. [Validating the Model Performance: Function](#section04)
5. [Main Function](#section05)
    * [Initializing WandB](#section501)
    * [Importing and Pre-Processing the domain data](#section502)
    * [Creation of Dataset and Dataloader](#section503)
    * [Neural Network and Optimizer](#section504)
    * [Training Model and Logging to WandB](#section505)
    * [Validation and generation of Summary](#section506)
6. [Examples of the Summary Generated from the model](#section06)


#### Technical Details

This script leverages on multiple tools designed by other teams. Details of the tools used below. Please ensure that these elements are present in your setup to successfully implement this script.

- **Data**:
	- We are using the News Summary dataset available at [Kaggle](https://www.kaggle.com/sunnysai12345/news-summary)
	- This dataset is the collection created from Newspapers published in India, extracting, details that are listed below.  We are referring only to the first csv file from the data dump: `news_summary.csv`
	- There are`4514` rows of data.  Where each row has the following data-point:
		- **author** : Author of the article
		- **date** : Date the article was published
		- **headline**: Headline for the published article
		- **read_more** : URL for the article to follow online
		- **text**: This is the summary of the article
		- **ctext**: This is the complete article


- **Language Model Used**: 
    - This notebook uses one of the most recent and novel transformers model ***T5***. [Research Paper](https://arxiv.org/abs/1910.10683)    
    - ***T5*** in many ways is one of its kind transformers architecture that not only gives state of the art results in many NLP tasks, but also has a very radical approach to NLP tasks.
    - **Text-2-Text** - According to the graphic taken from the T5 paper. All NLP tasks are converted to a **text-to-text** problem. Tasks such as translation, classification, summarization and question answering, all of them are treated as a text-to-text conversion problem, rather than seen as separate unique problem statements.
    - **Unified approach for NLP Deep Learning** - Since the task is reflected purely in the text input and output, you can use the same model, objective, training procedure, and decoding process to ANY task. Above framework can be used for any task - show Q&A, summarization, etc. 
   - We will be taking inputs from the T5 paper to prepare our dataset prior to fine tuning and training.    
   - [Documentation for python](https://huggingface.co/transformers/model_doc/t5.html)




- Hardware Requirements: 
	- Python 3.6 and above
	- Pytorch, Transformers and
	- All the stock Python ML Library
	- GPU enabled setup 
   

- **Script Objective**:
	- The objective of this script is to fine tune ***T5 *** to be able to generate summary, that a close to or better than the actual summary  while ensuring the important information from the article is not lost.

---
