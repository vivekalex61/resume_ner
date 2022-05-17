
# Resume parser
[![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/tterb/atomic-design-ui/blob/master/LICENSEs)

Building a parser tool using Transformers, Python and basic natural language processing techniques.
The parser can extract Names, Phone numbers, Email IDs, Education and Skills from resumes.


## Introduction 

#### Resume
A resume is a brief summary of your skills and experience over one or two pages while a CV is more detailed and a longer representation of what the applicant is capable of doing.
Resumes are a great example of unstructured data. Since there is no widely accepted resume layout; They all may have different formats.
![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/cv.jpg)
                
## Overview 
- Extracting text from PDF:
- Data Preprocessing
- Model creation

### Datasets and Data-Loading
This dataset is a document annotation dataset to be used to perform NER on resumes from indeed.com
The dataset has 220 items of which 220 items have been manually labeled.

The labels are divided into following 10 categories:

Name,
College Name,
Degree,
Graduation Year,
Years of Experience,
Companies worked at,
Designation,
Skills,
Location,
Email Address,

link : https://www.kaggle.com/datasets/dataturks/resume-entities-for-ner

sample:

![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/resume_dataset_3.png)

### Data Preprocessing
 Preprocessing of data includes 
 
 1)Removing unwanted symbols and value
 2)removing trailing spaces

### Model building and training

#### 1)Bert transformer
BERT stands for Bidirectional Encoder Representations from Transformers. It is designed to pre-train deep bidirectional representations from unlabeled text by jointly conditioning on both left and right context. As a result, the pre-trained BERT model can be fine-tuned with just one additional output layer to create state-of-the-art models for a wide range of NLP task

For training we have used 'bert-base-uncased'

link : https://jonathan-hui.medium.com/nlp-bert-transformer-7f0ac397f524

![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/bert.png)

#### 2)Bert tokenizer

A tokenizer is in charge of preparing the inputs for a model. 
We have used fast version of the tokenizer.
 a “Fast” implementation based on the Rust library from hugging faceTokenizers. The “Fast” implementations allows:

a significant speed-up in particular when doing batched tokenization and

additional methods to map between the original string (character and words) and the token space (e.g. getting the index of the token comprising a given character or the span of characters corresponding to a given token).

we have downloaded tokenizer files locally  https://huggingface.co/bert-base-uncased/tree/main and download vocab.txt

#### Training

1)Tokenized the traing data using BERT tokenizer

2)configured BERT 

3)Trained the model for 20 epochs

3)Added predicted files into JSON format

#### Evaluation

1)Extracting text data from the resume using  tesseract OCR

2)Tokenized the extracted data using BERT tokenizer

3)Loading BERT model

4)predicting entities

3)Convert prediction prediction into JSON format
## Results
Below are the results  got from trained transformer.

![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/resume_text.png)

![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/pred.png)

## End Notes

The predictions are not upto the mark. The main reason is because of little data.
It will  perform well if we have atleast 1000 training sampples.


