# MLNotes
Notes on using/applying machine learning 

## Data Cleaning 
* [A simple way](http://www.kdnuggets.com/2017/02/removing-outliers-standard-deviation-python.html) to deal with outliers python 

## Feature Engineering
* **Numerical:** log, log(1+x), normalization, binarization 
* **Categorical:** one-hot encode, TF-IDF(text), weight of evidence 
* **Timeseries:** stats, MFCC(audio), FFT
* **Numerical/Timeseries** to categorical - RF/GBM

## Loss Functions 
* Squared loss minimizes expectation. Pick it when learning expected return on a stock.
* Logistic loss minimizes probability. Pick it when learning probability of click on advertisement.
* Hinge loss minimizes the 0,1 / yes-no question. Pick it when you want a hard prediction.
* Quantile loss minimizes the median. Pick it when you want to predict house prices.
* Ensembling multiple loss functions

Adapted from: https://github.com/JohnLangford/vowpal_wabbit/wiki/Loss-functions

## Initialization 
* If you are usin ReLu, it is god practice to initialize them with slightly positive bias to avoid dead neurons.

## Optimization 
* If we have a high learning rate, (basic) SGD has big steps and it is progressing fast. Solution: use decaying learning rate; ADAM and such.  

![Learning rate too high](https://raw.githubusercontent.com/spartonia/MLNotes/master/static/lrate.png "Spikes in Accuracy: high learning rate")


## Regularization
#### Overfitting:
Causes: 
* Too many neurons
* Not enough data 
* Bad network 

To cure overfitting: 
* Dropout (note: some noise may come back. Not recommended with conv nets.)
* Data augmentation(add noise to data) 

#### Batch normalization 
Data in real world: large values, different scales, skewed, correlated

Solution:

1. Data whitening:
   * Scale: center around zero 
   * Decorrelate: (A+B)/2, A-B (PCA etc) 
   * Add an additional layer and let NN do it (to determine what the clean data is)

2. Batch normalization (better option) 
   * Works better than whitening 
   * How to: 
![Batch Normalization](https://raw.githubusercontent.com/spartonia/MLNotes/master/static/batchNormalization.png "Batch Normalization done right")

Note: 
* with batch normalization, bete replace bias so don't use bias when batch normalizing. 
* you can use higher lrate 
* stop using (or do a little) dropout 

