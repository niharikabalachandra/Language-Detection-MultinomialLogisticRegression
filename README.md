# Language-Detection
Language Detection using the European Parliament Proceedings Parallel Corpus. European Parliament Proceedings Parallel Corpus is a text dataset used for evaluating language detection engines. The 1.5GB corpus includes 21 languages spoken in EU.  This project aims to build a machine learning model trained on this dataset to predict new unseen data.

The Training data can be downloaded [here](http://www.statmt.org/europarl/). Be sure to download the source resource (file size: 1.5 GB)

Ask yourself why would they have selected this problem for the challenge? What are some gotchas in this domain I should know about?

What is the highest level of accuracy that others have achieved with this dataset or similar problems / datasets ?

What types of visualizations will help me grasp the nature of the problem / data?

What feature engineering might help improve the signal?

Which modeling techniques are good at capturing the types of relationships I see in this data?

Now that I have a model, how can I be sure that I didn't introduce a bug in the code? If results are too good to be true, they probably are!

What are some of the weakness of the model and and how can the model be improved with additional work?

## Step 1: Reading the files from individual folders as part of data extraction
Step 2: Removing noise from Training data

## Step 2: Removing noise from Training data
Preprocessing includes removing punctuations and digits from the extracted text.

## Step 3: Removing noise from Test data
We ensure that we treat the test data exactly like we treated the training data to remove characters such as punctuations and digits which add noise to test data

## Language Detection

List of all the languages whose detection is supported:
- 'bg': Bulgarian
- 'cs': Czech
- 'da': Danish
- 'de': German
- 'el': Greek, Modern 
- 'en': English
- 'es': Spanish
- 'et': Estonian
- 'fi': Finnish
- 'fr': French
- 'hu': Hungarian
- 'it': Italian
- 'lt': Lithuanian
- 'lv': Latvian
- 'nl': Dutch
- 'pl': Polish
- 'pt': Portuguese
- 'ro': Romanian
- 'sk': Slovak
- 'sl': Slovenian
- 'sv': Swedish

There are therefore, 21 categorical variables that our classifier needs to be able to identify correctly.

## Step 4: Function used to join all words held in a dataframe for a given language and place these words in a list

## Step 5: Converting the list 't', of all lists of strings, from every language, into a single dataframe. 
This dataframe "trainingData" is the Training data that we train our model on.

## Step 6: Building the model and training it with the training data
Character frequency analysis is undertaken using a logistic regressing model. Bi-gram model of word pairs is considered. We use a pipeline to implement this model and we use all CPU cores to build the model. L2 regularization is used to prevent overfitting of the model to training data. The inverse of regularization strength "C" is set to 1.0. Thereby, the model generalizes to new unseen data.

## Step 7: Using the trained model to make predictions on the Test data

## Analysis of result

The crosstab below shows us the false positives and false negatives that gives us some insight into correlation between languages. "P" stands for Predicted values and "A" stands for Actual values in the crosstab. 
- 502 strings in Slovak where missclassified as Czech. This points at the two languages being highly correlated. This makes sense since Czech Republic and Slovakia have a shared history contributing to similartes between the two languages spoken in this region. 

Similarly the following prominent trends emerged:
- 170 Spanish strings were missclassified as Portuguese
- 73 Italian strings were missclassified as Romanian
- 57 Swedish strings were missclassified as Danish
- 53 Italian strings were missclassified as Portuguese
- 43 Danish strings were missclassified as Dutch

## Analysis of Model

      labels   precision   recall   f1-score   support

         bg       1.00      1.00      1.00       997
         cs       0.62      0.98      0.76       993
         da       0.90      0.90      0.90       994
         de       0.89      0.96      0.92       993
         el       1.00      1.00      1.00       988
         en       0.96      0.89      0.92       998
         es       0.93      0.72      0.81       996
         et       0.95      0.83      0.88       993
         fi       0.88      0.99      0.93       995
         fr       0.94      0.93      0.93       999
         hu       0.95      0.99      0.97       998
         it       0.96      0.79      0.87       996
         lt       0.91      0.96      0.94       995
         lv       0.98      0.98      0.98       978
         nl       0.83      0.94      0.88       999
         pl       0.98      0.99      0.98       997
         pt       0.79      0.94      0.86       996
         ro       0.88      0.96      0.92       927
         sk       0.97      0.41      0.58       929
         sl       0.95      0.93      0.94       998
         sv       0.96      0.86      0.91       996 
     avg/total    0.92      0.90      0.90     20755
     
     0.903444953023

### Prediction accuracy of 90.344% was achieved on test data using a model trained with logistic regression 

# Inference

The European Parliment corpus is sizable at about 5 GB. This would seem to be a data at scale problem requiring Big Data analysis. However, by means of sampling we can execute the language detection classifier on a regular PC using the SciPy stack. Around 26.5 MB of text files were randomly selected for each language and analysis was carried out for this subsample (~554 MB) of the 5 GB corpus. We are able to still get a model accuracy of 90.344%, with the model generalizing to new unseen data. 
