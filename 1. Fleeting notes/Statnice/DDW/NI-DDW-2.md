**Zpracování a získávání informace z webu: předzpracování textu, reprezentace textu pomocí vektorů a modelů, extrakce informace z textu, extrakce pojmenovaných entit, analýza sentimentu.**

# Text Mining
Extracting information from text previously unknown. There are problems:
- High dimensionality
- Synonyms
- Ambiguity
- Context
- Lack of structure
- Highly redundant data

## Preprocessing
We process the input to make it easier for machines to work with.
### Tokenization
Grouping sequence of symbols together into a logical element (token).
Problems with certain symbols:
- '.'
	- delimiter (Hello.)
	- not delimiter in numbers (1.234)
	- token when part of abbreviation (E.G.)
- '
	- quote ('boom')
	- part of word (it's)
	- terminator (Tess')
### Stemming + Lemmatization + Stop words
Techniques to reduce dimensionality

Lemmatization = finding canonical form (are, is, am = be)
Stemming = finding the root of the word (waiting = wait)
Stop words = remove stop words that don't provide anything (a, the)
## Sentence Splitting
Not an easy task, we can split on every '.' but there are words and other elements that contain . without delimiting a sentence (we can have a list of such words to fight against it).
## N-Grams
Set of $N$ words in a given window.

Hello there, how are you? -> `{(Hello, there), (there, ','), (',', how), (how, are)...}`
### Applications
**Collocations:** We can get words that occur together.
**Generating text:** Get the last N-gram and generate the next word based on the probability.
## Part-Of-Speech Tagging
Assigning linguistic categories to words:
- NN - noun
- PNP - proper noun
- JJ - adjective
- VB - verb
- ...
## Phrase Detection/Chunking
Grouping tokens together. Process of finding a pattern in the text based on the POS tagging:
`<JJ>*<NN>` - get phrases with X adjectives followed by a noun
## Named Entity Recognition
Identifying entities in the text. They can be further classified as a certain type of entity - these categories can be fixed or dynamic based on the text.
### Entity Disambiguation
Detecting that two entities are in fact the same one. We can apply semantic web approaches to do this and assign URIs to these entities (entity linking).
### Relation Extraction
Extracting semantic relation between two entities. We can use POS tagging for this approach and find patterns in the text.
# Opinion Mining
Studying opinions, sentiment, emotions, attitudes from text. To make things easier we can focus on classifying as *positive, negative (and neutral)*.
1. Opinion extraction
2. Sentiment analysis
3. Opinion summarisation
## Sentiment Analysis
- Classifying as positive, negative and neutral. 
- Only focusing on certain topic (review on phone -> get sentiment on the screen, battery separately)
- Finding sentiment about some entity
- Opinion spam detection (detecting fake reviews)

### Lexicon-based
Have a list of positive and negative words and calculate their occurrences.

**Problems:**
- Opposite orientation - words can have different meanings (camera sucks, vacuum cleaner sucks)
- Sentiment words + No sentiment sentence - Which camera is good? (good = positive, but it's not)
- Sarcasm - What a great car! It broke after 1 drive
- No sentiment words - Car uses a lot of gas (probably bad, but not recognised)
### Supervised Sentiment Learning
Train on annotated data: reviews on the internet is a good start. Focus on sentiment words.
### Unsupervised Sentiment Learning
Classification based on fixed syntactic phrases (JJ NN - POS tagging to select the phrase)

We then find the sentiment orientation of the phrase based on some 2 reference words ("excellent", "poor"):
### $SO = log_2(\frac{\#(phrase\ NEAR\ excellent)\#(poor)}{\#(phrase\ NEAR\ poor)\#(excellent)})$
- \# - number of matching documents
- NEAR - search for documents that contain the words within 10 words of another
### Lexicon Expansion
Start with a lexicon and then expand it by finding similar words/synonyms/antonyms
# Text Summarisation
Reduce text to only include important information.
## Baseline Single Document Summarisation
1. Detect most important words and use top N
2. For each sentence find clusters of important words that are close to each other
3. Calculate score of the sentence
4. Return top sentences
# Vector Models

## Boolean Model
Vectors only have 0 or 1; only exact match is considered
## Vector Space Model
### TF-IDF
It is a method of creating a vector representation of a document
**TF** - term frequency
- How many times the term appears in the document
- $\#\ Term\ Appearences\ /\ \# Terms$ (in document)
**IDF** - inverse document frequency
- Measures how common a word is among all documents
- $log(\#\ Documents /\#\ Documents\ with \ Term)$
Celkem: $TF \times IDF$
### Jaccard Coefficient
Simple scoring approach:
### $score = \frac{|docA \cap docB|}{|docA \cup docB|}$
It doesn't consider term frequency 
### Euclidean Based Similarity
Calculate the classical distance between two documents.

It is not a good approach as scaling matters.
### Cosine Based Similarity
Measures the angle between two vectors.
Similarity is low when the angle is low.

# NLP
It's about classifying whole sentences.

## Word Embeddings
Representing a word as a vector.
Similar words are closer in the vector space; vector operations with words.

### Word2Vec
Shallow neural network to create the embedding based on n-grams.


