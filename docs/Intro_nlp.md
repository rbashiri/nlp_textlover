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


### Language Representations
#### sparse vectors (TF-IDF) 
The word "the" might appear 50 times in a single review. The word "brilliant" might appear twice. Which word tells you more about whether the reviewer liked the movie?

Obviously "brilliant" matters more. But bag of words would give "the" a value of 50 and "brilliant" a value of 2. The math is backwards. The most frequent words are often the least informative.

TF-IDF captures this intuition mathematically. A word is important to a document when:

It appears frequently in that document (term frequency)
It appears rarely across other documents (inverse document frequency)
Words that are common everywhere (like "the") get downweighted. Words that are common in one document but rare overall get boosted. This surfaces the words that make each document distinctive.
`Term Frequency(TF)`: How Often Does the Word Appear Here?
``` text
TF = t / n
```
Where:

t = number of times the word appears in the document
n = total number of words in the document

`Inverse Document Frequency`(IDF): How Rare Is This Word Overall?
```text
IDF = log(D / d)
```
Where:

D = total number of documents in the corpus
d = number of documents containing this word

```text 
The final score multiplies term frequency by inverse document frequency:
TF-IDF = TF × IDF
```
Limitations of TF-IDF
TF-IDF improves on raw word counts, but it still has limitations:

No understanding of meaning. "Happy" and "joyful" are treated as completely unrelated words. TF-IDF doesn't know they're synonyms.

No word order. Like bag of words, TF-IDF ignores sequence. "Not good" and "good not" produce identical scores.

Sparse vectors. Most words don't appear in most documents, so TF-IDF vectors are mostly zeros. This can be inefficient for very large vocabularies.

New vocabulary problems. Words that never appeared in your corpus get no representation at all.

Despite these limitations, TF-IDF remains widely used because it's fast, interpretable, and effective. It's often the first approach to try before moving to more complex methods like word embeddings.
### Calculation of TF-IDF
 TF-IDF by using the sklearn library. The `TfidfVectorizer()` class can be found in the sklearn. Import it this way:
 ```python
 # improt Tfidfvectorizer
 from sklearn.feature_extraction.text import TfidfVectorizer
  # step 2: create a counter and define stop words 
  stop_words = set(stopwords.words('english'))
count_tf_idf = TfidfVectorizer(stop_words=stop_words)
# step 3 Call the fit_transform() function to calculate the TF-IDF for the text corpus:
tf_idf = count_tf_idf.fit_transform(corpus)
# we can calculate ngram by passing the ngram_range argument to TfidfVectorizer().
 ```
### Word Embeddings:
`Word embeddings are a way of turning words into numbers that a computer can work with — but in a way that captures meaning, not just identity.`

- Start with your documents (reviews, sentences, articles — whatever collection of text you're working with).
- Scan through every single document and collect every unique word used anywhere in the whole collection
- That collected list of unique words IS the vocabulary
- Now that you know the vocabulary, you go back and convert each document into a vector, using that vocabulary as the fixed set of columns/slots. 

## From Sparse to Dense
A dense vector is simply a list of numbers where most or all of the values are non-zero — as opposed to a "sparse vector," where most values are zero.

- TF-IDF produces sparse vectors. If your vocabulary has 50,000 words, each document becomes a vector with 50,000 dimensions, mostly filled with zeros. Only the words that actually appear get non-zero values.

- A sparse vector is a vector (a list of numbers) where most of the values are zero, and only a small number of positions actually have a non-zero value.

- Simple definition
"Sparse" = mostly empty. Out of all the slots in the vector, only a few are "filled in" with real numbers — the rest are just 0.

-Word embeddings take a different approach. Each word becomes a dense vector with a fixed number of dimensions, typically between 100 and 300. Every dimension has a value. No zeros.

| Representation   | Dimensions | Values                          |
|------------------|------------|----------------------------------|
| TF-IDF           | 50,000+    | Mostly zeros, few non-zero      |
| Word Embedding   | 100–300    | All dimensions have values      |

*pre-trained embeddings*
- Word2Vec: often 300 from google
- GloVe: comes in 50, 100, 200, or 300-dimension versions: GloVe (Global - - Vectors for Word Representation)
- FastText: often 300 : Facebook extends Word2Vec 
- `BERT` stands for Bidirectional Encoder Representations from Transformers
**These pre-trained embeddings give you a starting point.**

Meaning Emerges from Context:
Word embeddings learn from these patterns. By analyzing billions of sentences, the algorithm discovers which words appear in similar contexts and places them near each other in vector space.

-embeddings aren't just placing similar words near each other randomly — they're capturing relationships (gender, tense, geography, comparison) as consistent, reusable directions in space.

-word embeddings is that relationships between words become mathematical operations.
What is "Corpora"?
Corpora is just the plural of "corpus"! 📚

1 corpus = a single collection of text documents
Many corpora = multiple collections of text documents

**Limitations of Word Embeddings**
Traditional word embeddings have one significant limitation: each word gets exactly one vector, regardless of context.
Modern approaches like `BERT` and other transformer models address this by creating contextual embeddings, where a word's vector depends on the surrounding sentence. But that's a topic for a later lesson.

#### Word2Vec:
The core idea is elegantly simple: train a neural network to predict words from their context. The embeddings emerge as a byproduct of this prediction task.
*The Core Insight: Context Predicts Meaning*
The context constrains what words make sense.
Word2Vec exploits this observation.

`Word2Vec comes in two versions that flip the prediction task:`

`CBOW (Continuous Bag of Words)` predicts the center word from surrounding context words. Given "adopted," "fluffy," "from," "shelter," predict that the missing word is "dog."

`Skip-gram` does the opposite. Given the center word, predict the surrounding context. Given "dog," predict that "adopted," "fluffy," "shelter" might appear nearby.

`Hint`:Skip-gram tends to work better for rare words and smaller datasets. CBOW trains faster on large datasets. In practice, skip-gram is more commonly used.

`The Context Window`

Skip-gram looks at words within a window around each target word. The window size determines how many neighbors count as context.
    - Slide the window one word to the right,
    
# Text Classification Pipeline Using Embeddings

1. **Tokenize each document**
   Split every document into a list of words. A materials abstract like "Efficient photocatalyst for solar hydrogen production" becomes a token list. Apply the same tokenization to every document in your dataset.

2. **Look up word embeddings**
   For each token, retrieve its vector from a pre-trained embedding set (Word2Vec, GloVe) or one you've trained yourself. Words with similar meaning end up with similar vectors, even if they never appeared together in your own dataset.

3. **Collapse words into one document vector**
   Average all the word vectors in a document to get a single fixed-length vector. For better results, weight the average by TF-IDF (or drop stopwords first) so distinctive terms like "photocatalyst" or "electrolyte" count more than "the" or "a".

4. **Feed document vectors into a classifier**
   Once every document is a fixed-length vector with a label, it's an ordinary supervised learning problem. Logistic regression or gradient boosting both work well as a first pass.

5. **Handle out-of-vocabulary words**
   Decide upfront what happens when a word isn't in your embedding vocabulary — skip it, substitute an "unknown" vector, or use FastText, which builds vectors for unseen words from subword pieces (useful for chemical naming variants).

6. **Evaluate against a simpler baseline**
   Compare your embedding-based classifier against plain TF-IDF. Embeddings tend to win when your labeled data is limited or test documents use different wording than training documents; TF-IDF tends to win when you have abundant data and exact keywords matter.

   ```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        MACHINE LEARNING PIPELINE                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   1. RAW TEXT          2. PREPROCESSING        3. FEATURE EXTRACTION       │
│   ─────────────        ───────────────         ──────────────────────      │
│   "The quick brown     "quick brown fox"       [0.2, 0.0, 0.8, ...]        │
│    fox jumps..."       (cleaned tokens)        (numbers!)                  │
│                                                                             │
│                                                                             │
│   4. TRAIN MODEL       5. MAKE PREDICTIONS     6. EVALUATE                 │
│   ──────────────       ──────────────────      ────────────                │
│   Learn patterns       New text → Category     How accurate?               │
│   from examples                                                            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```
