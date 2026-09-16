# Stemming in NLP

This project demonstrates **Stemming**, an important text preprocessing technique used in **Natural Language Processing (NLP)**.

The project covers three stemming techniques available in **NLTK**:

* Porter Stemmer
* Regexp Stemmer
* Snowball Stemmer

---

## What is Stemming?

**Stemming** is the process of reducing a word to its **root or base form** by removing prefixes or suffixes.

The resulting word is called a **stem**. The stem does not always have to be a grammatically correct English word.

### Example

```text
playing → play
played  → play
plays   → play
```

Another example:

```text
studies → studi
```

Here, `studi` is not a proper English word, but it is the stem produced by the stemming algorithm.

---

# 1. Porter Stemmer

**Porter Stemmer** is one of the most commonly used stemming algorithms.

It uses a set of rules to remove common English suffixes.

### Import

```python
from nltk.stem import PorterStemmer
```

### Example

```python
from nltk.stem import PorterStemmer

ps = PorterStemmer()

words = ["playing", "played", "plays", "studies", "running", "happily"]

for word in words:
    print(word, "->", ps.stem(word))
```

### Example Output

```text
playing -> play
played -> play
plays -> play
studies -> studi
running -> run
happily -> happili
```

### Key Point

Porter Stemmer is:

* Simple
* Fast
* Widely used
* Rule-based

---

# 2. Regexp Stemmer

**RegexpStemmer** uses a **regular expression (regex)** to remove a specified pattern from words.

Unlike Porter Stemmer, we can define the pattern ourselves.

### Import

```python
from nltk.stem import RegexpStemmer
```

### Example

```python
from nltk.stem import RegexpStemmer

rs = RegexpStemmer("ing$|s$|ed$")

words = ["playing", "playing", "played", "plays", "cars"]

for word in words:
    print(word, "->", rs.stem(word))
```

### How it works

The regex:

```text
ing$|s$|ed$
```

means:

* `ing$` → remove `ing` from the end
* `s$` → remove `s` from the end
* `ed$` → remove `ed` from the end

For example:

```text
playing → play
played  → play
cars    → car
```

### Important

RegexpStemmer is highly customizable because **you define the rule yourself**.

However, because the rules are manually defined, it may produce incorrect stems.

---

# 3. Snowball Stemmer

**Snowball Stemmer** is a more advanced stemming algorithm.

It is also sometimes called the **English Stemmer** and generally provides improved stemming compared with the original Porter algorithm.

### Import

```python
from nltk.stem import SnowballStemmer
```

### Example

```python
from nltk.stem import SnowballStemmer

ss = SnowballStemmer("english")

words = ["playing", "played", "plays", "studies", "running", "happily"]

for word in words:
    print(word, "->", ss.stem(word))
```

### Example Output

```text
playing -> play
played -> play
plays -> play
studies -> studi
running -> run
happily -> happili
```

Snowball Stemmer also supports multiple languages.

For example:

```python
SnowballStemmer("english")
SnowballStemmer("french")
SnowballStemmer("spanish")
```

---

# Comparison

| Feature      | Porter Stemmer | Regexp Stemmer       | Snowball Stemmer   |
| ------------ | -------------- | -------------------- | ------------------ |
| Type         | Rule-based     | Regex-based          | Rule-based         |
| Custom Rules | No             | Yes                  | No                 |
| Speed        | Fast           | Fast                 | Fast               |
| Flexibility  | Medium         | High                 | Medium             |
| Languages    | Mainly English | Depends on regex     | Multiple languages |
| Complexity   | Simple         | Simple               | Moderate           |
| Common Use   | General NLP    | Custom preprocessing | General NLP        |

---

# Stemming vs Lemmatization

Stemming and lemmatization both try to reduce words to their base form, but they work differently.

| Stemming                                  | Lemmatization                  |
| ----------------------------------------- | ------------------------------ |
| Removes parts of words using rules        | Finds the meaningful base word |
| Usually faster                            | Usually slower                 |
| Can produce invalid words                 | Usually produces valid words   |
| Does not require deep linguistic analysis | Uses linguistic information    |
| `studies → studi`                         | `studies → study`              |

### Example

```text
Stemming:
studies → studi

Lemmatization:
studies → study
```

---

# Why is Stemming Used?

Stemming can reduce the number of unique words in a dataset.

It is useful in:

* Text classification
* Search engines
* Information retrieval
* Sentiment analysis
* Text preprocessing
* Document similarity

For example:

```text
connect
connected
connecting
connection
```

A stemming algorithm may reduce several of these words to similar stems, making text processing easier.

---

# Installation

Install NLTK using:

```bash
pip install nltk
```

Then import the required stemmers:

```python
from nltk.stem import PorterStemmer
from nltk.stem import RegexpStemmer
from nltk.stem import SnowballStemmer
```

---

# Advantages of Stemming

* Easy to implement
* Fast
* Reduces vocabulary size
* Useful for preprocessing text
* Helps group different forms of words

# Limitations of Stemming

* May produce meaningless words
* May remove too much of a word
* Does not understand the meaning of words
* Different algorithms can produce different stems
* Manually defined regex rules can produce incorrect results

---

# Project Objective

The objective of this project is to understand:

1. What stemming is
2. Why stemming is used in NLP
3. How **PorterStemmer** works
4. How **RegexpStemmer** works
5. How **SnowballStemmer** works
6. The difference between different stemming algorithms
7. The difference between stemming and lemmatization

---

# Technologies Used

* Python
* NLTK
* Regular Expressions
* Jupyter Notebook

---

# Conclusion

Stemming is an important preprocessing technique in NLP that reduces words to their stems.

In this project, three NLTK stemmers were explored:

```text
PorterStemmer
      ↓
Rule-based stemming

RegexpStemmer
      ↓
Custom regex-based stemming

SnowballStemmer
      ↓
Improved rule-based stemming
```

Each stemmer has its own approach and can produce different results for the same word.

Understanding these algorithms provides a foundation for further **NLP preprocessing and text-processing tasks**.
