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

## Analysis of models

### Note:
Character frequency analysis and Word frequency analysis is undertaken using a logistic regressing model. n-gram models tested for include:
- 1-gram Character frequency analysis
- 2-gram Character frequency analysis
- 4-gram Character frequency analysis
- 1-gram Word frequency analysis
- 2-gram Word frequency analysis

We use a pipeline to implement these models and we use all CPU cores to build the models. L2 regularization is used to prevent overfitting of the models to training data. The inverse of regularization strength "C" is set to 1.0 for all models. Thereby, the models generalize to new unseen data.

### Analysis of 1-gram Character Model

       labels  precision    recall  f1-score   support

         bg       1.00      1.00      1.00       997
         cs       0.49      0.96      0.65       993
         da       0.85      0.79      0.82       994
         de       0.78      0.89      0.83       993
         el       1.00      1.00      1.00       988
         en       0.81      0.72      0.76       998
         es       0.75      0.51      0.61       996
         et       0.90      0.71      0.80       993
         fi       0.84      0.96      0.90       995
         fr       0.91      0.72      0.81       999
         hu       0.91      0.97      0.94       998
         it       0.90      0.48      0.63       996
         lt       0.78      0.94      0.85       995
         lv       0.95      0.94      0.95       978
         nl       0.64      0.90      0.75       999
         pl       0.95      0.97      0.96       997
         pt       0.69      0.85      0.76       996
         ro       0.73      0.88      0.80       927
         sk       0.73      0.20      0.31       929
         sl       0.90      0.80      0.85       998
         sv       0.93      0.75      0.83       996
     avg/total    0.83      0.81      0.80     20755

0.808961695977

#### Prediction accuracy of 80.896% was achieved on test data using a model trained with 1-gram Character logistic regression Model

### Analysis of 2-gram Character Model

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

#### Prediction accuracy of 90.344% was achieved on test data using a model trained with 2-gram Character logistic regression Model 

### Analysis of 4-gram Character Model

       labels  precision    recall  f1-score   support

         bg       1.00      1.00      1.00       997
         cs       0.68      0.98      0.80       993
         da       0.93      0.93      0.93       994
         de       0.91      0.98      0.94       993
         el       1.00      1.00      1.00       988
         en       0.99      0.92      0.95       998
         es       0.98      0.83      0.90       996
         et       0.97      0.87      0.92       993
         fi       0.90      0.99      0.95       995
         fr       0.97      0.95      0.96       999
         hu       0.95      0.99      0.97       998
         it       0.98      0.88      0.93       996
         lt       0.93      0.97      0.95       995
         lv       0.99      0.99      0.99       978
         nl       0.90      0.95      0.92       999
         pl       0.98      0.99      0.98       997
         pt       0.85      0.97      0.91       996
         ro       0.92      0.98      0.95       927
         sk       0.99      0.53      0.69       929
         sl       0.96      0.95      0.95       998
         sv       0.97      0.89      0.93       996
     avg / total  0.94      0.93      0.93     20755

0.931775475789

#### Prediction accuracy of 93.1775% was achieved on test data using a model trained with 4-gram Character logistic regression Model

### Analysis of 1-gram Word Model

       labels   precision   recall  f1-score   support

         bg       1.00      1.00      1.00       997
         cs       0.85      0.50      0.63       993
         da       0.96      0.89      0.92       994
         de       0.94      0.97      0.95       993
         el       0.63      1.00      0.78       988
         en       0.92      0.96      0.94       998
         es       0.83      0.72      0.77       996
         et       0.93      0.88      0.90       993
         fi       0.91      0.82      0.86       995
         fr       0.72      0.79      0.75       999
         hu       0.98      0.94      0.96       998
         it       0.86      0.92      0.89       996
         lt       0.97      0.84      0.90       995
         lv       0.79      0.91      0.85       978
         nl       0.52      0.94      0.67       999
         pl       0.95      0.81      0.87       997
         pt       0.47      0.56      0.51       996
         ro       0.99      0.84      0.91       927
         sk       0.91      0.71      0.79       929
         sl       0.78      0.44      0.56       998
         sv       0.98      0.89      0.93       996
     avg / total  0.85      0.83      0.83     20755

0.825439653096

#### Prediction accuracy of 82.5439% was achieved on test data using a model trained with 1-gram Word logistic regression Model

### Analysis of 2-gram Word Model

       labels  precision    recall  f1-score   support

         bg       1.00      1.00      1.00       997
         cs       0.85      0.49      0.62       993
         da       0.96      0.89      0.92       994
         de       0.94      0.97      0.95       993
         el       0.62      1.00      0.77       988
         en       0.91      0.96      0.94       998
         es       0.83      0.72      0.77       996
         et       0.93      0.88      0.90       993
         fi       0.91      0.82      0.86       995
         fr       0.71      0.79      0.75       999
         hu       0.99      0.94      0.96       998
         it       0.86      0.92      0.89       996
         lt       0.97      0.83      0.89       995
         lv       0.79      0.90      0.84       978
         nl       0.52      0.94      0.67       999
         pl       0.95      0.81      0.87       997
         pt       0.47      0.57      0.51       996
         ro       0.99      0.84      0.91       927
         sk       0.91      0.70      0.79       929
         sl       0.78      0.44      0.56       998
         sv       0.98      0.89      0.93       996
     avg / total  0.85      0.82      0.83     20755

0.823849674777

#### Prediction accuracy of 82.3849% was achieved on test data using a model trained with 2-gram Word logistic regression Model

## Comparison of all the models 

#### The comparison shown below is in terms of test data prediction accuracy

![Alt text](https://github.com/niharikabalachandra/Language-Detection/blob/master/accuracy.png)

## Analysis of result for 4-gram Character Model

The crosstab below shows us the false positives and false negatives that gives us some insight into correlation between languages. "P" stands for Predicted values and "A" stands for Actual values in the crosstab. 
- 399 strings in Slovak where missclassified as Czech. This points at the two languages being highly correlated. This makes sense since Czech Republic and Slovakia have a shared history contributing to similartes between the two languages spoken in this region. 

Similarly the following prominent trends emerged:
- 114 Spanish strings were missclassified as Portuguese
- 68 Estonian strings were missclassified as Finnish
- 44 Swedish strings were missclassified as Danish
- 42 Italian strings were missclassified as Romanian
- 30 Italian strings were missclassified as Portuguese
- 28 Dutch strings were missclassified as German
- 22 Danish strings were missclassified as Dutch
- 22 Estonian strings were missclassified as Lithuanian

![Alt text](https://github.com/niharikabalachandra/Language-Detection/blob/master/Crosstab.png)

# Inference 

The European Parliment corpus is sizable at about 5 GB. This would seem to be a data at scale problem requiring Big Data analysis. However, by means of sampling we can execute the language detection classifier on a regular PC using the SciPy stack. Around 26.5 MB of text files were randomly selected for each language and analysis was carried out for this subsample (~554 MB) of the 5 GB corpus. We are able to still get a model accuracy of 93.1775%, with the model generalizing to new unseen data. 
