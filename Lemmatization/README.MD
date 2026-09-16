# Lemmatization in NLP

## What is Lemmatization?

**Lemmatization** is an NLP text preprocessing technique used to convert a word into its **base or dictionary form**, known as a **lemma**.

Unlike stemming, lemmatization does not simply remove characters from the beginning or end of a word. It tries to understand the **meaning, vocabulary, and grammatical role** of a word to find its correct base form.

### Example

```text
running  → run
ran      → run
better   → good
studies  → study
children → child
```

The important point is that the result of lemmatization is generally a **valid dictionary word**.

For example:

```text
Stemming:
studies → studi

Lemmatization:
studies → study
```

`studi` is not a valid English word, while `study` is the actual base form.

---

# Why Do We Need Lemmatization?

A single word can appear in many different forms in a sentence.

For example:

```text
The boy is running.
The boy ran yesterday.
The boy runs every morning.
```

These words:

```text
running
ran
runs
```

represent the same basic concept: **run**.

If we process them as completely different words, our vocabulary becomes larger.

Lemmatization can normalize them:

```text
running → run
ran     → run
runs    → run
```

This can help NLP systems treat different grammatical forms of a word as related.

---

# How Lemmatization Works

Lemmatization generally involves more linguistic information than stemming.

A simplified process looks like this:

```text
Input Word
    ↓
Identify the word
    ↓
Determine grammatical information
    ↓
Use vocabulary / linguistic rules
    ↓
Find the base form
    ↓
Lemma
```

For example:

```text
"better"
   ↓
Adjective
   ↓
Dictionary / linguistic knowledge
   ↓
"good"
```

Another example:

```text
"children"
     ↓
Plural noun
     ↓
Dictionary knowledge
     ↓
"child"
```

This is why lemmatization can handle some words that simple suffix removal cannot.

---

# Lemma vs Root Word

A **lemma** is the canonical dictionary form of a word.

For example:

| Word     | Lemma |
| -------- | ----- |
| running  | run   |
| ran      | run   |
| runs     | run   |
| studies  | study |
| studied  | study |
| children | child |
| mice     | mouse |
| better   | good  |

The lemma does not necessarily have to be created by simply removing letters.

For example:

```text
better → good
```

You cannot get `good` by removing a suffix from `better`.

The relationship requires linguistic knowledge.

---

# Lemmatization Using NLTK

NLTK provides a class called **WordNetLemmatizer** for lemmatization.

### Import

```python
from nltk.stem import WordNetLemmatizer
```

Create an object:

```python
lemmatizer = WordNetLemmatizer()
```

Then:

```python
word = "running"

result = lemmatizer.lemmatize(word)

print(result)
```

Output:

```text
running
```

This result may seem surprising.

Why didn't:

```text
running → run
```

happen?

The reason is that **WordNetLemmatizer needs the correct Part of Speech (POS)** for many words.

---

# Part of Speech (POS)

POS tells us the grammatical role of a word.

Common POS categories include:

| POS       | Meaning                       | Example   |
| --------- | ----------------------------- | --------- |
| Noun      | Person, place, thing          | boy       |
| Verb      | Action                        | run       |
| Adjective | Describes a noun              | beautiful |
| Adverb    | Describes an action/adjective | quickly   |

The same word can have different meanings depending on its POS.

For example:

```text
"running"
```

can be interpreted as a noun or a verb depending on the sentence.

Therefore, providing the correct POS can improve lemmatization.

---

# WordNetLemmatizer with POS

Example:-

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

print(lemmatizer.lemmatize("running", pos="v"))
print(lemmatizer.lemmatize("studies", pos="v"))
print(lemmatizer.lemmatize("better", pos="a"))
```

Output:

```text
run
study
good
```

Here:

```text
v → verb
a → adjective
```

So:

```text
running + verb → run
studies + verb → study
better + adjective → good
```

---

# Important POS Tags in WordNet

WordNet uses specific characters for POS.

| WordNet POS | Meaning             |
| ----------- | ------------------- |
| `n`         | Noun                |
| `v`         | Verb                |
| `a`         | Adjective           |
| `r`         | Adverb              |
| `s`         | Satellite adjective |

Example:

```python
lemmatizer.lemmatize("cars", pos="n")
```

Output:

```text
car
```

And:

```python
lemmatizer.lemmatize("running", pos="v")
```

Output:

```text
run
```

---

# Downloading WordNet

NLTK's `WordNetLemmatizer` uses the **WordNet lexical database**.

Download it using:

```python
import nltk

nltk.download("wordnet")
nltk.download("omw-1.4")
```

Then:

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

word = "studies"

print(lemmatizer.lemmatize(word, pos="v"))
```

Output:

```text
study
```

---

# Examples of Lemmatization

```python
from nltk.stem import WordNetLemmatizer

lemmatizer = WordNetLemmatizer()

words = [
    ("running", "v"),
    ("ran", "v"),
    ("studies", "v"),
    ("children", "n"),
    ("mice", "n"),
    ("better", "a")
]

for word, pos in words:
    print(word, "→", lemmatizer.lemmatize(word, pos=pos))
```

Possible output:

```text
running → run
ran → run
studies → study
children → child
mice → mouse
better → good
```

---

# Stemming vs Lemmatization

This is one of the most important differences in NLP preprocessing.

### Stemming

Stemming usually works by applying rules to remove prefixes or suffixes.

```text
studies → studi
```

The result may not be a valid word.

### Lemmatization

Lemmatization uses linguistic information to find the proper base form.

```text
studies → study
```

The result is generally a valid dictionary word.

### Comparison

| Feature              | Stemming                         | Lemmatization                      |
| -------------------- | -------------------------------- | ---------------------------------- |
| Approach             | Removes word endings             | Finds dictionary base form         |
| Linguistic knowledge | Low                              | Higher                             |
| Speed                | Generally faster                 | Generally slower                   |
| Output               | May be invalid word              | Usually valid word                 |
| Context              | Usually doesn't consider context | Can use POS/linguistic information |
| Example              | `studies → studi`                | `studies → study`                  |
| Complexity           | Simple                           | More complex                       |

---

# Example: Why Lemmatization is Better for Some Words

Consider:

```text
The children are playing.
```

A stemming algorithm might produce:

```text
children → children
playing → play
```

But lemmatization can use vocabulary knowledge:

```text
children → child
playing → play
```

Another example:

```text
The mice are eating cheese.
```

Lemmatization:

```text
mice → mouse
eating → eat
```

This shows an important advantage of lemmatization.

The base form is not always obtained by simply cutting characters.

---

# Lemmatization and Context

Lemmatization can depend on the grammatical role of a word.

Consider:

```text
"The meeting was better."
```

Here `better` is an adjective.

```python
lemmatizer.lemmatize("better", pos="a")
```

Result:

```text
good
```

However, without specifying the appropriate POS, the result may not be what we expect.

Therefore, **POS tagging and lemmatization are often used together** in NLP pipelines.

---

# Lemmatization Pipeline

A typical NLP preprocessing pipeline can look like:

```text
Raw Text
   ↓
Tokenization
   ↓
POS Tagging
   ↓
Lemmatization
   ↓
Clean / Normalized Text
   ↓
Machine Learning / NLP Task
```

For example:

```text
Original Sentence:
"The children were running quickly."

        ↓

Tokenization:
["The", "children", "were", "running", "quickly"]

        ↓

POS Information:
children → noun
were → verb
running → verb
quickly → adverb

        ↓

Lemmatization:
children → child
were → be
running → run
quickly → quickly
```

Result:

```text
["The", "child", "be", "run", "quickly"]
```

The exact output depends on the POS information and lemmatizer being used.

---

# Advantages of Lemmatization

### 1. Produces Meaningful Words

Lemmatization generally produces valid dictionary words.

```text
studies → study
children → child
mice → mouse
```

### 2. Uses Linguistic Information

It can use the grammatical role of a word.

```text
running + verb → run
better + adjective → good
```

### 3. Better Normalization

Different forms of a word can be mapped to a common base form.

```text
run
runs
running
ran
```

can be normalized toward:

```text
run
```

### 4. Useful for NLP Tasks

Lemmatization can be useful in:

* Search engines
* Text classification
* Sentiment analysis
* Information retrieval
* Question answering
* Document similarity
* Chatbots
* Text preprocessing

---

# Limitations of Lemmatization

### 1. Slower Than Stemming

Lemmatization generally requires more processing and linguistic information than simple stemming.

### 2. Requires Linguistic Resources

Tools such as WordNet depend on dictionaries or lexical databases.

### 3. POS Matters

Incorrect or missing POS information can lead to unexpected results.

For example:

```python
lemmatizer.lemmatize("running")
```

may not return:

```text
run
```

whereas:

```python
lemmatizer.lemmatize("running", pos="v")
```

returns:

```text
run
```

### 4. Language Dependent

The quality of lemmatization depends on the language and the available linguistic resources.

---

# When Should We Use Lemmatization?

Lemmatization is useful when **meaning and linguistic correctness are important**.

For example, if we are processing:

```text
"The children are studying."
```

we may want:

```text
child
study
```

rather than potentially incorrect stems.

Stemming can be preferred when:

```text
Speed and simplicity
```

are more importa
