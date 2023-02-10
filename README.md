# Introduction-to-Arabic-Text-Processing
Introduction to Arabic Text Processing
# Installation steps
*************************************************************************************
pip install camel-tools -f https://download.pytorch.org/whl/torch_stable.html
*************************************************************************************
from google.colab import drive
import os

drive.mount('/gdrive')
*************************************************************************************
%mkdir /gdrive/MyDrive/camel_tools
os.environ['CAMELTOOLS_DATA'] = '/gdrive/MyDrive/camel_tools'

!export | camel_data -i all
*************************************************************************************
pip install camel-tools

from google.colab import drive
import os

drive.mount('/gdrive')
os.environ['CAMELTOOLS_DATA'] = '/gdrive/MyDrive/camel_tools'
*************************************************************************************
## Word Tokenization
sentence = "هَلْ ذَهَبْتَ إِلَى المُحاضَرة؟"
print(sentence)

sent_split = sentence.split()
print(sent_split)
*************************************************************************************
## Morphological
from camel_tools.morphology.database import MorphologyDB
from camel_tools.morphology.analyzer import Analyzer

# First, we need to load a morphological database.
# Here, we load the default database which is used for analyzing
# Modern Standard Arabic. 
db = MorphologyDB.builtin_db()

analyzer = Analyzer(db)

analyses = analyzer.analyze('معلم')

for analysis in analyses:
    print(analysis, '\n')
*************************************************************************************
## Sentiment Analysis
from camel_tools.sentiment import SentimentAnalyzer

sa = SentimentAnalyzer.pretrained()

sentences = [
    'أنا سعيد',
    'أنا لست سعيد'
]

sentiments = sa.predict(sentences)

print(sentiments)
*************************************************************************************
## Named Entitiy Recognition
from camel_tools.tokenizers.word import simple_word_tokenize
from camel_tools.ner import NERecognizer

ner = NERecognizer.pretrained()

# NERecognizer expects pre-tokenized text
sentence = simple_word_tokenize('ولاية نيويورك هي إحدى ولايات دولة الولايات المتحدة الأمريكية الخمسين.')

labels = ner.predict_sentence(sentence)

# Print each token paired with it's NER label
print(list(zip(sentence, labels)))
*************************************************************************************
# Dialect Identification
from camel_tools.dialectid import DialectIdentifier

did = DialectIdentifier.pretrained()

sentences = [
'والله ما كان على بالي يا هوى
قمرين، قمرين دول ولا عينيك
قلبي بيسألني عليك
أتاريني بافكر فيك'
]

predictions = did.predict(sentences, 'city')
print([p.top for p in predictions])

predictions = did.predict(sentences, 'country')
print([p.top for p in predictions])

predictions = did.predict(sentences, 'region')
print([p.top for p in predictions])
*************************************************************************************
*************************************************************************************
*************************************************************************************
*************************************************************************************
*************************************************************************************
*************************************************************************************
