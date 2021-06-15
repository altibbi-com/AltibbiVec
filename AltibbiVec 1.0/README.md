## AltibbiVec 1.0

 
AltibbiVec is a domain-specific word embedding model for health and medical-related content in the Arabic context. AltibbiVec can be applied to various NLP applications to serve the research community in the medical NLP in Arabic.

It is developed based on three well-known word embedding techniques: Word2Vec, FastText, and GloVe. Besides, it is trained with more than 1.8 million medical consultations and questions obtained from Altibbi's databases. Altibbi is a telemedicine company that provides the MENA region with simplified medical and health knowledge alongside telehealth services.

The three developed models were evaluated by word clustering, word similarity, and question classification based on the specialty type. The question classification was performed by the BiLSTM neural classifier. Hence, Word2Vec and FastText performed the best in similarity and word clustering, whereas FastText had the best result regarding the question classification.

This model can be improved further by using BERT and language models as more data is available.


## How To Use
These models were built using [gensim](https://radimrehurek.com/gensim/) Python library. Here's a simple code for loading and using
one of the models by following these steps:
1. Install `gensim` >= **3.4** and `nltk` >= **3.2** using either `pip` or `conda`

>> pip install gensim nltk

>> conda install gensim nltk

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


### FastText Models
 | Docs No.             | Vocabs No.    | Dimension		| Download      |
 | --------             | ----------          | ---------	    | --------- 	|
 | 8,253,725              | 270,301              | **100**	        | [Download](https://drive.google.com/file/d/1a9frdABNNZAkocbUzGm8C5K2zP9w1q0O/view?usp=sharing)  |
