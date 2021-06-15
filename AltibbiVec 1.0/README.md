## AltibbiVec 1.0

 
AltibbiVec is a domain-specific word embedding model for health and medical-related content in the Arabic context. AltibbiVec can be applied to various NLP applications to serve the research community in the medical NLP in Arabic.

It is developed based on three well-known word embedding techniques: Word2Vec, FastText, and GloVe, and across three dimensions: 100, 200, and 300. Besides, it is trained with more than 1.8 million medical consultations and questions obtained from Altibbi's databases. Altibbi is a telemedicine company that provides the MENA region with simplified medical and health knowledge alongside telehealth services.

The three developed models were evaluated by word clustering, word similarity, and question classification based on the specialty type. The question classification was performed by the BiLSTM neural classifier. Hence, Word2Vec and FastText performed the best in similarity and word clustering, whereas FastText had the best result regarding the question classification. 

Generally, the best obtained models were at dimenion **100**. The developed models can be improved further by using BERT and language models as more data is available.

## Prerequisites

The [gensim](https://radimrehurek.com/gensim/) Python library was used to tokenize and build the Word2Vec. 
In order to use AltibbiVec-Word2Vec you need to install it.

1. Install `gensim` >= **3.4** and `nltk` >= **3.2** using either `pip` or `conda`

>> pip install gensim nltk

>> conda install gensim nltk

To use AltibbiVec-FastText, install the FastText library using Google Colaboratory:

>>!pip install fasttext

or
>> pip install fasttext

>> conda install -c conda-forge fasttext

To use AltibbiVec-Glove, install the Glove library using:

>>pip install glove_python

## How To Use
Here's a simple code for loading and using one of the models by following these steps:

2. extract the compressed model files to a directory [ e.g. `Altibbi-FastText` ]
3. keep the **.npy** files, alongside the **.mdl**. You are gonna to load the file with no extension, like what you'll see in the following code.
4. run this python code to load and use the model

```python

# -*- coding: utf8 -*-
import gensim
import re

# load the model
model = gensim.models.Word2Vec.load('Altibbi-FastText')

# Clean/Normalize Arabic Text
def clean_str(text):
    chars = '[٠١٢٣٤٥٦٧٨٩0123456789[؟|$|.|!_،,@!#%^&*();<>":``.//\',\']'
    text = re.sub(r'[^\w]+', ' ', text)
    text = re.sub(r'[a-zA-Z]', r'', text)
    text = re.sub(chars, r'', str(text))
    text = re.sub(r'\s+', r' ', text, flags=re.I)  # remove multiple spaces with single space
    text = text.replace('وو', 'و')
    text = text.replace('يي', 'ي')
    text = text.replace('اا', 'ا')
    text = text.replace('\n', ' ')

    return text

word = clean_str(u'المعده')

# find and print the most similar terms to a word
most_similar = model.wv.most_similar( word )
for term, score in most_similar:
	print(term, score)
	
# get a word vector
word_vector = model.wv[ word ]

# find the cosine similarity between the vectors for any two words.
print(model.wv.similarity(w1='المعده', w2='البطن'))


```

## Download

### Word2Vec Model
 | Docs No.    |Unique vocabs |Structure|  | Dimension	 | Download|
 | --------    | -------      | --------   | ---------	 | --------- |
 | 1,464,411   |166,293       |Skip gram   | **100**     | [Download](https://drive.google.com/file/d/1-YdvvxEQWxrLgn2tsoS7nvjbz2cn4XOn/view?usp=sharing)  |
 | 1,464,411   |166,293       |Skip gram   | **200**	 | [Download](https://drive.google.com/file/d/1dHxzcy2PhlX4abHMFvHew01gLhllpCDn/view?usp=sharing)  |
 | 1,464,411   |166,293       |Skip gram   | **300**	 | [Download](https://drive.google.com/file/d/1RFCe3voj6u3W9argTSahB9R3T7P9ojlj/view?usp=sharing)  |

### FastText Model
 | Docs No.    |Unique vocabs |Structure| | Dimension	| Download  |
 | --------    | -------      | --------  | ----------  | --------- |  
 | 1,464,411   |166,293       |CBOW       | **100**	| [Download](https://drive.google.com/file/d/1a9frdABNNZAkocbUzGm8C5K2zP9w1q0O/view?usp=sharing)  |
 | 1,464,411   |166,293       |CBOW       | **200**	| [Download](https://drive.google.com/file/d/1F7dI9LvbxTupO21sOXG630U1SM1bEoXv/view?usp=sharing)  |
 | 1,464,411   |166,293       |CBOW       | **300**	| [Download](https://drive.google.com/file/d/1nzAs8pWFae6nFrr0vRQ-VwoGUHnBTqa0/view?usp=sharing)  |  
 
 
 ### GloVe Model
 | Docs No.  |Unique vocabs       | Dimension		| Download  |
 | --------  | -------            | ----------          | --------- |  
 | 1,464,411 |166,293             | **100**	        | [Download](https://drive.google.com/file/d/1oQaSzo5ZARuv4uKq9g73MU-PUeCq1P-B/view?usp=sharing)  |
 | 1,464,411 |166,293             | **200**	        | [Download](https://drive.google.com/file/d/1-1seHUxp7C6CS9sR8nTWisvhQEYR7yHg/view?usp=sharing)  |
 | 1,464,411 |166,293             | **300**	        | [Download](https://drive.google.com/file/d/1-2x1oZEngFCXBeM3c3XfyLrf2Izm9uSy/view?usp=sharing)  |  
