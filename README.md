# Word-predictor: language model algorithm and word prediction app

## Presentation

### Introduction

* The problem: Smartphones are everywhere. People type on them often. But text entry on a touchscreen is painful.

* The solution: A word prediction app guesses the next word you're going to type. This saves you time and effort. And it's fun.

* A new app has been developed for this - word prediction. It's in the prototype stage, where it is stable and fast.

* The prototype is available on the Web for you try. The app is built in English, and it can easily be adapted to other languages.

* The app does more than just predict. It also gives you insight into its magic – you can play with parameters interactively.

### Technical Details

* App was trained on 3 document sets – 100 million words from Twitter, news, and blogs. 80% for training, 20% for testing.

* Probabilistic models were built with 1-4 word sequences ('n-grams'). Models were smoothed statistically for accuracy.

* Optimized app:

    * 'Trie' data structure is used for speed and space.
    * Singleton word sequences are filtered out.
    * Words are stored as index keys to save space.
    * Probabilities are quantized logarithms to save space.
    * App was created in RStudio with quanteda tools and new code. On a MacBook Pro, model build time was 4 hours.

### Conclusion

* You can try the app yourself at shinyapps.io. Just type a phrase into the box to get a prediction. Predictions will appear immediately.

        http://dmodjeska.shinyapps.io/predict_app/

* To get more insight into the app, you can play with some of its settings interactively. For example, you can set the app to use all word sources or only Twitter.

* With additional support, this app can be developed into a product on the market. All that's needed is some statistics, some QA, and some TLC. And lots of words.

* We hope that you're intrigued. Thanks for your time!

## About

* Inputs for this app's language model were 3 corpora of approximately 200 MB each from Twitter, news, and blogs. (The data comes from [HC Corpora](http://www.corpora.heliohost.org/).) 80% samples were used, with 20% reserved for testing. Ngram models were created from these corpora using strings of 1-4 words. Good-Turing smoothing was then applied to account for unseen grams.

* A series of optimizations was made to produce a working model:

    * A trie data structure to reduce speed complexity to a constant value, and to trim redundant storage of ngram prefixes
    * Filtering out of ngrams whose instance count was 1, in order to improve prediction accuracy and reduce storage for uninformative features
    * Storing terms as integer keys into a master index, in order to reduce redundant language in the model
    * Converting term probabilities to quantized logarithms, in order to reduce the storage space required for double-precision, floating-point numbers
    * The app was created in RStudio using the quanteda package and custom code. Computation was performed on a MacBook Pro (mid-2014) with a 2.2 GHz quad-core CPU and 16 GB RAM. Computation time was approximately 4 hours to build the combined language model.

* Key references for this work were:

    * _Speech and Language Processing_ (second edition), by Jurafsky and Martin, chapter 4
    * _Statistical Machine Translation_ by Philipp Koehn, chapter 7

* This app was created for the capstone project in the Data Science specialization of Coursera.

## Files

### Language Model Algorithm

* [__model.R__](model.R) - get, pre-process, and tokenize corpora; build, smooth, and optimize n-gram models
* [__clean_words.R__](clean_words.R) - pre-process a corpus for encoding, punctuation, spacing, contractions, abbreviations, profanity, numbers, URL's, and spelling
* [__measure.R__](measure.R) - evaluate algorithm against test data
* [__predict.R__](predict.R) - use the language model to predict the next word in an input phrase
* [__swearWords.txt__](swearWords.txt) - a list of profanity

### Word Prediction App

* [__clean_words.R__](clean_words.R), [__predict.R__](predict.R), [__swearWords.txt__](swearWords.txt) - pre-processing and prediction files from the language model algorithm
* [__en_US.blogs.80trie.rds__](predict_app/en_US.blogs.80trie.rds), [__en_US.twitter.80trie.rds__](predict_app/en_US.twitter.80trie.rds), [__en_US.news.80trie.rds__](predict_app/en_US.news.80trie.rds), [__en_US.combo.80trie.rds__](predict_app/en_US.combo.80trie.rds) - language models for blogs, Twitter, news, and combined corpora
* [__ui.R__](predict_app/ui.R), [__server.R__](predict_app/server.R), [__styles.css__](predict_app/styles.css), [__smartphone65.png__](predict_app/www/smartphone65.png) - UI and server files for the Shiny app

### Presentation Deck

* [__predict_deck_2.Rpres__](predict_deck_rpres/predict_deck_2.Rpres), [__app_cap100B.png__](predict_deck_rpres/app_cap100B.png) - presentation deck in R Presenter format

## Instructions

* __Language model algorithm:__ Run model.R from an R command line or in RStudio, with clean_words.R in the same directory. Parameters can be adjusted at the top of predict.R for debugging, plotting, n-gram length, and training/testing percentages.
* __Word prediction app:__ Run the application using ui.R or server.R from an R command line or in RStudio, with the other app files in the same directory.
* __Presentation deck:__ Preview predict_deck_2.Rpres from an R command line or in RStudio, with the other presentation files in the same directory.
