
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

#### Evaluation metrics used

##### MUC-5 EVALUATION METRICS

The MUC-5 Scoring System is evaluation software that aligns and scores the templates produced by th e
information extraction systems under evaluation in comparison to an "answer key" created by humans . The Scoring
System produces comprehensive summary reports showing the overall scores for the templates in the test set ;

The basic scoring categories are found in the score report under the column headings COR, PAR, INC,
XCR, XPA, XIC, MIS, SPU, and NON.

• If the response and the key are deemed to be equivalent, the category is correct (COR); if interactively
assigned, a tally appears in both the COR and XCR (interactive correct) columns.
• If the response and the key are judged to be a near match, the category is partial (PAR) ; if interactively
assigned, a tally appears in both the PAR and XPA (interactive partial) columns .
• If the key and response do not match, the category is incorrect (INC) ; if interactively assigned, a tall y
appears in both the INC and XIC (interactive incorrect) columns.
• If the key has a fill and the response has no corresponding fill, the category is missing (MIS) .
• If the response has a fill which has no corresponding fill in the key, the category is spurious (SPU) .
• If the key and response are both left blank, then the category is noncommittal (NON) .

![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/MCU_Eval.png)

Types of scoring in MCU:

![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/manners_scoring.png)

Error Metrics in MCU:

![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/system_dept_err.png)
![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/recall_precision_metrics.png)
![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/fscore.png)


ref: https://aclanthology.org/M93-1007.pdf, https://www.davidsbatista.net/blog/2018/05/09/Named_Entity_Evaluation/


## Results
Below are the results  got from trained transformer.

![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/resume_text.png)

![alt text](https://raw.githubusercontent.com/vivekalex61/resume_ner/main/images/pred.png)

## End Notes

The predictions are not upto the mark. The main reason is because of little data.
It will  perform well if we have atleast 1000 training sampples.


