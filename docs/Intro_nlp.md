### What is Natural Language Processing?

**Natural Language Processing (NLP) is the field of artificial intelligence that gives machines the ability to read, understand, and generate human language.**

1- NLP is about extracting meaningful information from text and speech. 
2- When you summarize a long article for a friend in two sentences, that's NLP too

### Common NLP Tasks

*Table 1. Examples of common Natural Language Processing tasks and their outputs.*

| Task | Question It Answers | Example Output |
| --- | --- | --- |
| Classification | "What type of text is this?" | "This email is spam" |
| Sentiment Analysis | "What's the emotional tone?" | "This review is positive" |
| Named Entity Recognition | "What entities are mentioned?" | [Apple: ORG], [San Francisco: LOC] |
| Machine Translation | "What does this mean in another language?" | "Bonjour" -> "Hello" |
| Summarization | "What's the short version?" | A 3-sentence summary of a 10-page report |
| Question Answering | "What's the answer to this question?" | "The company was founded in 2004" |

**Tokenization: Breaking Text into Pieces**
1- Word Tokenization
2- Subword tokenization
3- Character tokenization
**Requirment**
1- Text Preprocessing
    - lowercasing
    - punctuation - keep punctuation as separate tokens preserves       information.
    - Stopword Removal: Stopwords are extremely common words that appear in almost every document: "the," "a," "an," "is," "are," "in," "on," "at," "to," "for," and so on.
        `Removing stopwords can help models focus on content words.`
    - Stemming : Stemming reduces words to their root form by chopping off endings. The idea is that "running," "runs," "ran," and "runner" all relate to the concept of "run."
    Stemmers don't produce actual words; they produce stems. They also miss irregular forms: "better" stays as "better" rather than connecting to "good."
    - Lemmatization :Lemmatization also reduces words to a base form, but it uses vocabulary and grammar rules to return actual words. The base form is called a `lemma`.

    *Table 2. Examples of words and their lemmatized forms.*

    | Original | Lemma |
    | --- | --- |
    | running | run |
    | runs | run |
    | easily | easily |
    | studies | study |
    | better | good |
    | went | go |


   *For quick prototypes and search applications, stemming is often good enough. For tasks where word meaning matters or when you need readable output, lemmatization is worth the extra effort* 

## The Preprocessing Pipeline
    In practice, preprocessing involves chaining multiple steps together. A typical pipeline might:
        1.	Convert to lowercase
        2.	Remove or separate punctuation
        3.	Tokenize into words
        4.	Remove stopwords
        5.	Apply lemmatization


`The trend in NLP is toward less aggressive preprocessing for powerful models and more traditional preprocessing for smaller models or specific applications like search.`

### The Teaching Library
    1- NLTk: 
    The Natural Language Toolkit, known as NLTK, is the grandfather of Python NLP libraries.

    2- spaCy: arrived in 2015 with a different philosophy: speed and practicality over comprehensiveness. Where NLTK offers five ways to do something, spaCy offers one way that works well and runs fast.

    3- Hugging Face Transformers:
    Hugging Face started as a chatbot company but pivoted to become the central hub for modern NLP. Their Transformers library provides easy access to thousands of pre-trained models including BERT, GPT, RoBERTa, T5, and nearly every other model you've heard of.

    4- Gensim:
    Gensim specializes in unsupervised learning for text. If you need to discover topics in a collection of documents, find similar documents, or work with word embeddings, Gensim is purpose-built for these tasks.

### Choosing the Right Library

With so many options, how do you choose? Here is a practical framework:

*Table 3. Recommended NLP libraries for common situations.*

| Situation | Recommended Library |
| --- | --- |
| Learning NLP concepts | NLTK |
| Building production pipelines | spaCy |
| Maximum accuracy on a task | Hugging Face Transformers |
| Topic modeling or document similarity | Gensim |
| Named entity recognition | spaCy or Hugging Face |
| Text classification | Hugging Face (best accuracy) or spaCy (good speed) |
| Sentiment analysis | Hugging Face (best) or TextBlob (quickest) |

*In practice, many projects use multiple libraries. You might use spaCy for fast preprocessing, Hugging Face for classification, and Gensim for finding similar documents. The libraries complement each other.*

## Setting Up spaCy

Install the spaCy library in your project's Python environment:

```bash
python -m pip install spacy
```

spaCy separates the library from its language models. After installing spaCy, download a model for each language you need. For English, run this command in the VS Code terminal:

```bash
python -m spacy download en_core_web_sm
```

This downloads the small English model. spaCy offers English models in different sizes:

*Table 4. Comparison of spaCy English language models.*

| Model | Size | Speed | Accuracy |
| --- | --- | --- | --- |
| `en_core_web_sm` | ~12 MB | Fastest | Good |
| `en_core_web_md` | ~40 MB | Fast | Better |
| `en_core_web_lg` | ~560 MB | Slower | Best |

## The spaCy Pipeline
`spaCy works differently from NLTK. Instead of calling separate functions for each task, you pass text through a pipeline that performs multiple analyses at once.`

``` python
    import spacy

    nlp = spacy.load('en_core_web_sm')

    text = "Apple is looking at buying a startup in San Francisco."
    doc = nlp(text)
```
*Neither approach is better. They serve different purposes. Use NLTK when learning concepts or when you need fine control. Use spaCy when building applications or processing large amounts of text.*

`Hint:`
Here are the steps for text preprocessing:
1.	`Tokenization`: you'll need to divide the text into tokens (separate phrases, words, and symbols);

2.	`Lemmatization`: you'll need to reduce the words to their root forms (lemma).
You can use these libraries for both tokenization and lemmatization:
    •	Natural Language Toolkit (NLTK)
    •	spaCy


## Import tokenizatoin function:

``` python
from nltk.tokenize import word_tokenize # import word_ tokenize
from nltk.stem import WordNetLemmatizer  # import WordNetLemmantizer
lemmatizer  = WordNetLemmatizer()

```
## Practical workflow

Think of the process like this:

`Raw text → lowercase → tokenize → lemmatize → join → corpus → later extract features → ML model`
| Step                      | What you do                            | Result/example                                    |
| ------------------------- | -------------------------------------- | ------------------------------------------------- |
| **1. Lowercase**          | Make capitalization consistent         | `Movies` → `movies`                               |
| **2. Tokenization**       | Break text into individual pieces      | `"movies were good"` → `['movies','were','good']` |
| **3. Lemmatization**      | Convert words toward their base form   | `movies` → `movie`                                |
| **4. Join**               | Put processed words back into a string | `['movie','be','good']` → `"movie be good"`       |
| **5. Corpus**             | Collect all reviews/texts              | thousands of processed reviews                    |
| **6. Feature extraction** | Comes **after this lesson**            | convert words into numbers                        |

### What is a corpus?

This is another important term from this lesson.

A corpus = collection of texts used for NLP analysis.

### regular expressions: `re`
Regular expressions (Regex) find text based on a pattern.Instead of searching for one exact word, Regex lets you describe what the text should look like.
 Regex to find or clean:
    - numbers
    - dates
    - email addresses
    - punctuation
    - unwanted symbols
    - specific character patterns

**re.sub() is especially important for NLP preprocessing.Find a pattern → replace it with something else**
 ``` python
 import re
# pattern
# substitution — what each pattern match should be substituted with
# text — the text which the function scans for pattern matches
re.sub(pattern, substitution, text)

 ```
 As part of the preprocessing step, we should remove all characters except letters, apostrophes, and spaces, so let's write a regular expression to find them.
 
 raw strings for Regex patterns.*r"..."*
 The `r` tells Python to treat backslashes literally, which prevents conflicts between Python escape characters and Regex syntax.

 ``` python
 re.sub(r"pattern", "replacement", text)
 ```

```text
Raw review
    ↓
Regex cleaning
    ↓
Tokenization
    ↓
Lemmatization
    ↓
Clean text
    ↓
Convert text to numerical features
    ↓
ML model
```
**Summary**

*Regular Expressions (Regex)*: Regex is a pattern-matching tool used to find, extract, replace, or remove parts of text. In NLP, it is commonly used during text preprocessing to remove unwanted characters such as punctuation, numbers, or symbols. Python provides the re module, and re.sub(pattern, replacement, text) can replace all text matching a pattern. Regex patterns are usually written as raw strings (r"...") to avoid problems with Python escape characters.

## Bag of Words — What you should learn

1. Why do we need Bag of Words?
 A machine-learning model cannot directly work with:
  "this movie is very good"
It needs numerical features.

workflow  is now:
``` text
Raw text
    ↓
Regex cleaning
    ↓
Tokenization
    ↓
Lemmatization
    ↓
Clean text
    ↓
Bag of Words
    ↓
Numerical features
    ↓
ML model
``` 
`Main lesson:Bag of Words (BoW) converts text into numerical features by counting how often words appear.`

*Note*: Bag of words doesnot know the order of words it only knows the number of words
N-grams: Preserving Some Word Order
N-grams offer a partial solution. Instead of treating each word independently, we consider sequences of consecutive words.

The "N" refers to how many words are in each sequence:

Unigrams (N=1): individual words, same as regular bag of words
Bigrams (N=2): two-word sequences
Trigrams (N=3): three-word sequences
Larger n-grams preserve more context, but they create many more features and usually require more data.

`Summary`

**Bag of Words** is an NLP technique that converts text into numerical features so that machine-learning models can process it.

### How it works

1. Create a **vocabulary** of unique words from the corpus.
2. Count how many times each vocabulary word appears in each text.
3. Represent each text as a numerical **vector**.
4. Combine the vectors into a **matrix** that can be used by an ML model.

```text
Clean text
    ↓
Create vocabulary
    ↓
Count word occurrences
    ↓
Create numerical vectors
    ↓
Feature matrix
    ↓
Machine-learning model
```

### Important Terms

* **Corpus:** Collection of texts/documents.
* **Vocabulary:** Unique words used as features.
* **Vector:** Numerical representation of one text.
* **Matrix:** Numerical representation of the whole corpus.
* **Unigram:** One-word feature.
* **Bigram:** Two consecutive words.
* **Trigram:** Three consecutive words.

### Limitation of Bag of Words

Bag of Words counts words but **does not preserve word order**. Therefore, some information about context and meaning is lost.

### N-grams

N-grams preserve some word order by treating consecutive words as features.

* `N = 1` → Unigram
* `N = 2` → Bigram
* `N = 3` → Trigram

Larger n-grams capture more context but also create more features and a sparser feature matrix.


# Bag of Words with CountVectorizer

## Purpose

`CountVectorizer()` converts a text corpus into numerical features that a machine-learning model can use.

### Basic Workflow

``` text
Clean/Lemmatized Corpus
        ↓
CountVectorizer()
        ↓
fit_transform(corpus)
        ↓
Create vocabulary
        ↓
Count word occurrences
        ↓
Bag-of-Words matrix
        ↓
ML features
```

## Important Code

**Import CountVectorizer**
``` python
from sklearn.feature_extraction.text import CountVectorizer

#Create the vectorizer
count_vect = CountVectorizer()

# Fit and transform the corpus( learn words and convert them)

bow = count_vect.fit_transform(corpus)

## Understanding `fit_transform()

# `fit` → learns the vocabulary from the corpus.
#`transform` → converts the texts into numerical features.
# `fit_transform` → performs both operations.

## Shape

bow.shape()

#The output:
(number of texts, number of vocabulary features)

Example:

(7, 16)

means:

# 7 texts
# 16 word features
```
## Vocabulary

The vocabulary contains the unique words used as features.
``` python
count_vect.get_feature_names_out()
```
Each vocabulary word represents one column in the Bag-of-Words matrix.
## N-grams
`ngram_range` controls how many consecutive words are treated as one feature.

* `(1, 1)` → unigrams only
* `(2, 2)` → bigrams only
* `(3, 3)` → trigrams only
* `(1, 2)` → unigrams and bigrams

Example:

`CountVectorizer(ngram_range=(2, 2))`

## Stop Words

Stop words are common words such as `the`, `a`, `of`, and `for` that may provide little useful information for some NLP tasks.

They can be removed to reduce unnecessary features.

stop_words = set(stopwords.words('english'))

Then:

`CountVectorizer(stop_words=stop_words)`

### Final Concept

**CountVectorizer = Text → Numerical Features**

It learns the vocabulary, counts word or n-gram occurrences, and creates the feature matrix that can be passed to a machine-learning model.
```