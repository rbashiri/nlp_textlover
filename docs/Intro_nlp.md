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



