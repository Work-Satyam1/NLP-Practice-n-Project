# NLP Tokenization Practice

This repository contains my practical implementation of **Tokenization using NLTK (Natural Language Toolkit)**.

The purpose of this practice is to understand how text is divided into smaller units such as **sentences and words**, which is an important first step in Natural Language Processing (NLP).

## Topics Covered

* Sentence Tokenization
* Word Tokenization
* WordPunct Tokenization
* Treebank Word Tokenization
* Tokenizing a complete paragraph
* Tokenizing individual sentences

## Technologies Used

* Python
* NLTK

## Installation

Install NLTK using pip:

```bash
pip install nltk
```

## 1. Creating a Corpus

A small text corpus was created for practicing different tokenization techniques.

```python
corpus = """Hello Welcome,to Krish Naik's NLP Tutorials.
Please do watch the entire course! to become expert in NLP.
"""
```

## 2. Sentence Tokenization

Sentence tokenization divides a paragraph into individual sentences.

```python
from nltk.tokenize import sent_tokenize

documents = sent_tokenize(corpus)

for sentence in documents:
    print(sentence)
```

### Output

```text
Hello Welcome,to Krish Naik's NLP Tutorials.
Please do watch the entire course!
to become expert in NLP.
```

### Concept

```text
Paragraph
   ↓
Sentence Tokenization
   ↓
Sentence 1
Sentence 2
Sentence 3
```

## 3. Word Tokenization

Word tokenization divides text into individual words and punctuation tokens.

```python
from nltk.tokenize import word_tokenize

word_tokenize(corpus)
```

### Output

```text
['Hello', 'Welcome', ',', 'to', 'Krish', 'Naik', "'s",
 'NLP', 'Tutorials', '.', 'Please', 'do', 'watch', 'the',
 'entire', 'course', '!', 'to', 'become', 'expert', 'in',
 'NLP', '.']
```

Word tokenization can also be applied sentence by sentence:

```python
for sentence in documents:
    print(word_tokenize(sentence))
```

## 4. WordPunct Tokenization

`wordpunct_tokenize()` separates words and punctuation more aggressively.

```python
from nltk.tokenize import wordpunct_tokenize

wordpunct_tokenize(corpus)
```

For example:

```text
Naik's
```

is tokenized as:

```text
Naik
'
s
```

This differs from `word_tokenize()`, which produces:

```text
Naik
's
```

## 5. Treebank Word Tokenizer

NLTK also provides the `TreebankWordTokenizer`.

```python
from nltk.tokenize import TreebankWordTokenizer

tokenizer = TreebankWordTokenizer()

tokenizer.tokenize(corpus)
```

This tokenizer follows rules based on the **Penn Treebank** tokenization conventions.

For example, contractions and punctuation are handled according to Treebank-style rules.

## Tokenization Comparison

| Tokenizer                 | Main Purpose                                      |
| ------------------------- | ------------------------------------------------- |
| `sent_tokenize()`         | Splits text into sentences                        |
| `word_tokenize()`         | Splits text into words and punctuation            |
| `wordpunct_tokenize()`    | Separates words and punctuation more aggressively |
| `TreebankWordTokenizer()` | Uses Penn Treebank-style tokenization rules       |

## Key Learning

Tokenization is the process of breaking text into smaller units called **tokens**.

For example:

```text
"Hello, world!"
```

can be broken into:

```text
["Hello", ",", "world", "!"]
```

Sentence tokenization:

```text
Paragraph
   ↓
Sentences
```

Word tokenization:

```text
Sentence
   ↓
Words + Punctuation
```

Tokenization is commonly used as an initial preprocessing step in NLP tasks such as:

* Text Classification
* Sentiment Analysis
* Named Entity Recognition
* Machine Translation
* Text Generation
* Information Retrieval

## Project Structure

```text
NLP-Tokenization/
│
├── tokenization.ipynb
└── README.md
```

## Conclusion

Through this practical, I learned how different NLTK tokenizers process text and how a paragraph can be divided into sentences, words, and punctuation tokens.
