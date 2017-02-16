# MLNotes
Notes on using/applying machine learning 


## Loss Functions 
* Squared loss minimizes expectation. Pick it when learning expected return on a stock.
* Logistic loss minimizes probability. Pick it when learning probability of click on advertisement.
* Hinge loss minimizes the 0,1 / yes-no question. Pick it when you want a hard prediction.
* Quantile loss minimizes the median. Pick it when you want to predict house prices.
* Ensembling multiple loss functions

Adapted from: https://github.com/JohnLangford/vowpal_wabbit/wiki/Loss-functions


## Optimization 
* If we have a high learning rate, SGD has ig steps and jumps back and forth. 

![Learning rate too high](https://raw.githubusercontent.com/spartonia/MLNotes/master/static/lrate.png "Spikes in Accuracy: high learning rate")

