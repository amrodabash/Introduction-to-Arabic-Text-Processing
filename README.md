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
from camel_tools.utils.dediac import dediac_ar
sentence = "هَلْ ذَهَبْتَ إِلَى المُحاضَرة؟"
print(sentence)

sent_split = sentence.split()
print(sent_split)
*************************************************************************************
Results:
هَلْ ذَهَبْتَ إِلَى المُحاضَرة؟
['هَلْ', 'ذَهَبْتَ', 'إِلَى', 'المُحاضَرة؟']
*************************************************************************************
## Morphological
from camel_tools.morphology.database import MorphologyDB
from camel_tools.morphology.analyzer import Analyzer

First, we need to load a morphological database.
Here, we load the default database which is used for analyzing
Modern Standard Arabic. 

db = MorphologyDB.builtin_db()

analyzer = Analyzer(db)

analyses = analyzer.analyze('معلم')

for analysis in analyses:
    print(analysis, '\n')
*************************************************************************************
Results:
{'diac': 'مَعْلَم', 'lex': 'مَعْلَم', 'bw': 'مَعْلَم/NOUN', 'gloss': 'sign;mark', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'i', 'cas': 'u', 'enc0': '0', 'rat': 'i', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مَعْلَم', 'caphi': 'm_a_3_l_a_m', 'd1tok': 'مَعْلَم', 'd2tok': 'مَعْلَم', 'pos_logprob': -0.4344233, 'd3tok': 'مَعْلَم', 'd2seg': 'مَعْلَم', 'pos_lex_logprob': -4.379362, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مَعْلَم', 'pattern': 'مَ1ْ2َ3', 'lex_logprob': -4.379362, 'atbtok': 'مَعْلَم', 'atbseg': 'مَعْلَم', 'd1seg': 'مَعْلَم', 'stem': 'مَعْلَم', 'stemgloss': 'sign;mark', 'stemcat': 'Ndu'} 

{'diac': 'مَعْلَمَ', 'lex': 'مَعْلَم', 'bw': 'مَعْلَم/NOUN+َ/CASE_DEF_ACC', 'gloss': 'sign;mark+[def.acc.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'c', 'cas': 'a', 'enc0': '0', 'rat': 'i', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مَعْلَمَ', 'caphi': 'm_a_3_l_a_m_a', 'd1tok': 'مَعْلَمَ', 'd2tok': 'مَعْلَمَ', 'pos_logprob': -0.4344233, 'd3tok': 'مَعْلَمَ', 'd2seg': 'مَعْلَمَ', 'pos_lex_logprob': -4.379362, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مَعْلَم_+َ', 'pattern': 'مَ1ْ2َ3َ', 'lex_logprob': -4.379362, 'atbtok': 'مَعْلَمَ', 'atbseg': 'مَعْلَمَ', 'd1seg': 'مَعْلَمَ', 'stem': 'مَعْلَم', 'stemgloss': 'sign;mark', 'stemcat': 'Ndu'} 

{'diac': 'مَعْلَمٌ', 'lex': 'مَعْلَم', 'bw': 'مَعْلَم/NOUN+ٌ/CASE_INDEF_NOM', 'gloss': 'sign;mark+[indef.nom.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'i', 'cas': 'n', 'enc0': '0', 'rat': 'i', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مَعْلَمٌ', 'caphi': 'm_a_3_l_a_m_u_n', 'd1tok': 'مَعْلَمٌ', 'd2tok': 'مَعْلَمٌ', 'pos_logprob': -0.4344233, 'd3tok': 'مَعْلَمٌ', 'd2seg': 'مَعْلَمٌ', 'pos_lex_logprob': -4.379362, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مَعْلَم_+ٌ', 'pattern': 'مَ1ْ2َ3ٌ', 'lex_logprob': -4.379362, 'atbtok': 'مَعْلَمٌ', 'atbseg': 'مَعْلَمٌ', 'd1seg': 'مَعْلَمٌ', 'stem': 'مَعْلَم', 'stemgloss': 'sign;mark', 'stemcat': 'Ndu'} 

{'diac': 'مَعْلَمِ', 'lex': 'مَعْلَم', 'bw': 'مَعْلَم/NOUN+ِ/CASE_DEF_GEN', 'gloss': 'sign;mark+[def.gen.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'c', 'cas': 'g', 'enc0': '0', 'rat': 'i', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مَعْلَمِ', 'caphi': 'm_a_3_l_a_m_i', 'd1tok': 'مَعْلَمِ', 'd2tok': 'مَعْلَمِ', 'pos_logprob': -0.4344233, 'd3tok': 'مَعْلَمِ', 'd2seg': 'مَعْلَمِ', 'pos_lex_logprob': -4.379362, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مَعْلَم_+ِ', 'pattern': 'مَ1ْ2َ3ِ', 'lex_logprob': -4.379362, 'atbtok': 'مَعْلَمِ', 'atbseg': 'مَعْلَمِ', 'd1seg': 'مَعْلَمِ', 'stem': 'مَعْلَم', 'stemgloss': 'sign;mark', 'stemcat': 'Ndu'} 

{'diac': 'مَعْلَمٍ', 'lex': 'مَعْلَم', 'bw': 'مَعْلَم/NOUN+ٍ/CASE_INDEF_GEN', 'gloss': 'sign;mark+[indef.gen.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'i', 'cas': 'g', 'enc0': '0', 'rat': 'i', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مَعْلَمٍ', 'caphi': 'm_a_3_l_a_m_i_n', 'd1tok': 'مَعْلَمٍ', 'd2tok': 'مَعْلَمٍ', 'pos_logprob': -0.4344233, 'd3tok': 'مَعْلَمٍ', 'd2seg': 'مَعْلَمٍ', 'pos_lex_logprob': -4.379362, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مَعْلَم_+ٍ', 'pattern': 'مَ1ْ2َ3ٍ', 'lex_logprob': -4.379362, 'atbtok': 'مَعْلَمٍ', 'atbseg': 'مَعْلَمٍ', 'd1seg': 'مَعْلَمٍ', 'stem': 'مَعْلَم', 'stemgloss': 'sign;mark', 'stemcat': 'Ndu'} 

{'diac': 'مَعْلَمُ', 'lex': 'مَعْلَم', 'bw': 'مَعْلَم/NOUN+ُ/CASE_DEF_NOM', 'gloss': 'sign;mark+[def.nom.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'c', 'cas': 'n', 'enc0': '0', 'rat': 'i', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مَعْلَمُ', 'caphi': 'm_a_3_l_a_m_u', 'd1tok': 'مَعْلَمُ', 'd2tok': 'مَعْلَمُ', 'pos_logprob': -0.4344233, 'd3tok': 'مَعْلَمُ', 'd2seg': 'مَعْلَمُ', 'pos_lex_logprob': -4.379362, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مَعْلَم_+ُ', 'pattern': 'مَ1ْ2َ3ُ', 'lex_logprob': -4.379362, 'atbtok': 'مَعْلَمُ', 'atbseg': 'مَعْلَمُ', 'd1seg': 'مَعْلَمُ', 'stem': 'مَعْلَم', 'stemgloss': 'sign;mark', 'stemcat': 'Ndu'} 

{'diac': 'مُعَلِّم', 'lex': 'مُعَلِّم', 'bw': 'مُعَلِّم/NOUN', 'gloss': 'teacher', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'i', 'cas': 'u', 'enc0': '0', 'rat': 'r', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مُعَلِّم', 'caphi': 'm_u_3_a_l_l_i_m', 'd1tok': 'مُعَلِّم', 'd2tok': 'مُعَلِّم', 'pos_logprob': -0.4344233, 'd3tok': 'مُعَلِّم', 'd2seg': 'مُعَلِّم', 'pos_lex_logprob': -3.844249, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مُعَلِّم', 'pattern': 'مُ1َ2ِّ3', 'lex_logprob': -3.844249, 'atbtok': 'مُعَلِّم', 'atbseg': 'مُعَلِّم', 'd1seg': 'مُعَلِّم', 'stem': 'مُعَلِّم', 'stemgloss': 'teacher', 'stemcat': 'Nall'} 

{'diac': 'مُعَلِّمَ', 'lex': 'مُعَلِّم', 'bw': 'مُعَلِّم/NOUN+َ/CASE_DEF_ACC', 'gloss': 'teacher+[def.acc.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'c', 'cas': 'a', 'enc0': '0', 'rat': 'r', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مُعَلِّمَ', 'caphi': 'm_u_3_a_l_l_i_m_a', 'd1tok': 'مُعَلِّمَ', 'd2tok': 'مُعَلِّمَ', 'pos_logprob': -0.4344233, 'd3tok': 'مُعَلِّمَ', 'd2seg': 'مُعَلِّمَ', 'pos_lex_logprob': -3.844249, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مُعَلِّم_+َ', 'pattern': 'مُ1َ2ِّ3َ', 'lex_logprob': -3.844249, 'atbtok': 'مُعَلِّمَ', 'atbseg': 'مُعَلِّمَ', 'd1seg': 'مُعَلِّمَ', 'stem': 'مُعَلِّم', 'stemgloss': 'teacher', 'stemcat': 'Nall'} 

{'diac': 'مُعَلِّمٌ', 'lex': 'مُعَلِّم', 'bw': 'مُعَلِّم/NOUN+ٌ/CASE_INDEF_NOM', 'gloss': 'teacher+[indef.nom.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'i', 'cas': 'n', 'enc0': '0', 'rat': 'r', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مُعَلِّمٌ', 'caphi': 'm_u_3_a_l_l_i_m_u_n', 'd1tok': 'مُعَلِّمٌ', 'd2tok': 'مُعَلِّمٌ', 'pos_logprob': -0.4344233, 'd3tok': 'مُعَلِّمٌ', 'd2seg': 'مُعَلِّمٌ', 'pos_lex_logprob': -3.844249, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مُعَلِّم_+ٌ', 'pattern': 'مُ1َ2ِّ3ٌ', 'lex_logprob': -3.844249, 'atbtok': 'مُعَلِّمٌ', 'atbseg': 'مُعَلِّمٌ', 'd1seg': 'مُعَلِّمٌ', 'stem': 'مُعَلِّم', 'stemgloss': 'teacher', 'stemcat': 'Nall'} 

{'diac': 'مُعَلِّمِ', 'lex': 'مُعَلِّم', 'bw': 'مُعَلِّم/NOUN+ِ/CASE_DEF_GEN', 'gloss': 'teacher+[def.gen.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'c', 'cas': 'g', 'enc0': '0', 'rat': 'r', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مُعَلِّمِ', 'caphi': 'm_u_3_a_l_l_i_m_i', 'd1tok': 'مُعَلِّمِ', 'd2tok': 'مُعَلِّمِ', 'pos_logprob': -0.4344233, 'd3tok': 'مُعَلِّمِ', 'd2seg': 'مُعَلِّمِ', 'pos_lex_logprob': -3.844249, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مُعَلِّم_+ِ', 'pattern': 'مُ1َ2ِّ3ِ', 'lex_logprob': -3.844249, 'atbtok': 'مُعَلِّمِ', 'atbseg': 'مُعَلِّمِ', 'd1seg': 'مُعَلِّمِ', 'stem': 'مُعَلِّم', 'stemgloss': 'teacher', 'stemcat': 'Nall'} 

{'diac': 'مُعَلِّمٍ', 'lex': 'مُعَلِّم', 'bw': 'مُعَلِّم/NOUN+ٍ/CASE_INDEF_GEN', 'gloss': 'teacher+[indef.gen.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'i', 'cas': 'g', 'enc0': '0', 'rat': 'r', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مُعَلِّمٍ', 'caphi': 'm_u_3_a_l_l_i_m_i_n', 'd1tok': 'مُعَلِّمٍ', 'd2tok': 'مُعَلِّمٍ', 'pos_logprob': -0.4344233, 'd3tok': 'مُعَلِّمٍ', 'd2seg': 'مُعَلِّمٍ', 'pos_lex_logprob': -3.844249, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مُعَلِّم_+ٍ', 'pattern': 'مُ1َ2ِّ3ٍ', 'lex_logprob': -3.844249, 'atbtok': 'مُعَلِّمٍ', 'atbseg': 'مُعَلِّمٍ', 'd1seg': 'مُعَلِّمٍ', 'stem': 'مُعَلِّم', 'stemgloss': 'teacher', 'stemcat': 'Nall'} 

{'diac': 'مُعَلِّمُ', 'lex': 'مُعَلِّم', 'bw': 'مُعَلِّم/NOUN+ُ/CASE_DEF_NOM', 'gloss': 'teacher+[def.nom.]', 'pos': 'noun', 'prc3': '0', 'prc2': '0', 'prc1': '0', 'prc0': '0', 'per': 'na', 'asp': 'na', 'vox': 'na', 'mod': 'na', 'stt': 'c', 'cas': 'n', 'enc0': '0', 'rat': 'r', 'source': 'lex', 'form_gen': 'm', 'form_num': 's', 'd3seg': 'مُعَلِّمُ', 'caphi': 'm_u_3_a_l_l_i_m_u', 'd1tok': 'مُعَلِّمُ', 'd2tok': 'مُعَلِّمُ', 'pos_logprob': -0.4344233, 'd3tok': 'مُعَلِّمُ', 'd2seg': 'مُعَلِّمُ', 'pos_lex_logprob': -3.844249, 'num': 's', 'ud': 'NOUN', 'gen': 'm', 'catib6': 'NOM', 'root': 'ع.ل.م', 'bwtok': 'مُعَلِّم_+ُ', 'pattern': 'مُ1َ2ِّ3ُ', 'lex_logprob': -3.844249, 'atbtok': 'مُعَلِّمُ', 'atbseg': 'مُعَلِّمُ', 'd1seg': 'مُعَلِّمُ', 'stem': 'مُعَلِّم', 'stemgloss': 'teacher', 'stemcat': 'Nall'} 


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
Results:
['positive', 'negative']

*************************************************************************************
## Named Entitiy Recognition
from camel_tools.tokenizers.word import simple_word_tokenize
from camel_tools.ner import NERecognizer

ner = NERecognizer.pretrained()

NERecognizer expects pre-tokenized text
sentence = simple_word_tokenize('ولاية نيويورك هي إحدى ولايات دولة الولايات المتحدة الأمريكية الخمسين.')

labels = ner.predict_sentence(sentence)

Print each token paired with it's NER label
print(list(zip(sentence, labels)))
*************************************************************************************
Results:
[('ولاية', 'O'), ('نيويورك', 'B-LOC'), ('هي', 'O'), ('إحدى', 'O'), ('ولايات', 'O'), ('دولة', 'O'), ('الولايات', 'B-LOC'), ('المتحدة', 'I-LOC'), ('الأمريكية', 'I-LOC'), ('الخمسين', 'O'), ('.', 'O')]

*************************************************************************************
## Dialect Identification
from camel_tools.dialectid import DialectIdentifier

did = DialectIdentifier.pretrained()

sentences = [
'والله ما كان على بالي يا هوى'
'قمرين، قمرين دول ولا عينيك'
'قلبي بيسألني عليك'
'أتاريني بافكر فيك'
]

predictions = did.predict(sentences, 'city')
print([p.top for p in predictions])

predictions = did.predict(sentences, 'country')
print([p.top for p in predictions])

predictions = did.predict(sentences, 'region')
print([p.top for p in predictions])
*************************************************************************************
Results:
['Cairo']
['Egypt']
['Nile Basin']
*************************************************************************************
