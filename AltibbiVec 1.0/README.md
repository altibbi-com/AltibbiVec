## AltibbiVec 1.0

## How To Use
These models were built using [gensim](https://radimrehurek.com/gensim/) Python library. Here's a simple code for loading and using
one of the models by following these steps:
1. Install `gensim` >= **3.4** and `nltk` >= **3.2** using either `pip` or `conda`

>> pip install gensim nltk

>> conda install gensim nltk

2. extract the compressed model files to a directory [ e.g. `Altibbi-FastText` ]
3. keep the **.npy** files. You are gonna to load the file with no extension, like what you'll see in the following code.
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
 | Docs No.             | Vocabularies No.    | Vec-Size		| Download      |
 | --------             | ----------          | ---------	    | --------- 	|
 | 8,253,725              | 270,301              | **20**	        | [Download]()  |
