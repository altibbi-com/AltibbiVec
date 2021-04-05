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
    text = str(text)
    
    search = ["أ","إ","آ","ة","_","-","/",".","،"," و "," يا ",'"',"ـ","'","ى","\\",'\n', '\t','&quot;','?','؟','!']
    replace = ["ا","ا","ا","ه"," "," ","","",""," و"," يا","","","","ي","",' ', ' ',' ',' ? ',' ؟ ',' ! ']
    
    #remove english words
    text = re.sub(r'[a-zA-Z]', r'', text)
    
    #remove tashkeel
    p_tashkeel = re.compile(r'[\u0617-\u061A\u064B-\u0652]')
    text = re.sub(p_tashkeel,"", text)
    
    #remove longation
    p_longation = re.compile(r'(.)\1+')
    subst = r"\1\1"
    text = re.sub(p_longation, subst, text)
    
    text = text.replace('وو', 'و')
    text = text.replace('يي', 'ي')
    text = text.replace('اا', 'ا')
    text = text.replace('\n', ' ')

    
    for i in range(0, len(search)):
        text = text.replace(search[i], replace[i])
    
    #trim    
    text = text.strip()

    return text

# python 3.X
word = clean_str(u'المعده')

# find and print the most similar terms to a word
most_similar = model.wv.most_similar( word )
for term, score in most_similar:
	print(term, score)
	
# get a word vector
word_vector = model.wv[ word ]

```

## Download


### Models

Model        	  | Docs No.             | Vocabularies No.    | Vec-Size		| Download      |
-----        	  | --------             | ----------          | ---------	    | --------- 	|
Altibbi-FastText          | 8253725           | 270301 | **20**	        | [Download]() |
Altibbi-FastText          | 8253725           | 270301 | **100**	    | [Download]() |
