# MLNotes
Notes on using/applying machine learning 

## Preprocessing and Data Cleaning 
* **Images (DL)**
   * Center (subtract the mean image or per channel mean)
   * Not common to dp PCA, normalizing etc. 

* [A simple way](http://www.kdnuggets.com/2017/02/removing-outliers-standard-deviation-python.html) to deal with outliers python 

#### Feature Engineering
* **Numerical:** log, log(1+x), normalization, binarization 
* **Categorical:** one-hot encode, TF-IDF(text), weight of evidence 
* **Timeseries:** stats, MFCC(audio), FFT
* **Numerical/Timeseries** to categorical - RF/GBM

## Architecture 
#### Loss Functions 
* Squared loss minimizes expectation. Pick it when learning expected return on a stock.
* Logistic loss minimizes probability. Pick it when learning probability of click on advertisement.
* Hinge loss minimizes the 0,1 / yes-no question. Pick it when you want a hard prediction.
* Quantile loss minimizes the median. Pick it when you want to predict house prices.
* Ensembling multiple loss functions

Adapted from: https://github.com/JohnLangford/vowpal_wabbit/wiki/Loss-functions

#### Initialization 
* If you are usin ReLu, it is good practice to 
   * initialize them with slightly positive bias to avoid dead neurons (small networks).
   * Xavier-He initialization `W = np.random.rand(fan_in, fan_out) / np.sqrt(fan_in/2)` (recommended).

## Training 
#### Optimization
* To sanity check the network, start witha very small data (20 images) and no regularization and overfit the model. You should be able to see `accuracy ~= 1` and `loss ~= 0` if everything is fine. 
* If we have a high learning rate, (basic) SGD has big steps and it is progressing fast. Solution: use decaying learning rate; ADAM and such.  
* decay lr overtime. 

![Learning rate too high](https://raw.githubusercontent.com/spartonia/MLNotes/master/static/lrate.png "Spikes in Accuracy: high learning rate")

###### Hyperparamter optimization  
1. Getting some ideas: in training, start with two extreme lrs (`1e-6`, `1e6`) and narrow it down by adjust it incremantally (binary search like) until the loss is declining in a sensible way (not staying flat, not exploding, no NaNs, exceptions etc).
2. Fine tuning: [here](https://youtu.be/GUtlrDbHhJM?list=PLlJy-eBtNFt6EuMxFYRiNRS07MCWN5UIA&t=3961)
3. Prefer random search over grid search. 

#### Regularization
###### Overfitting:
Causes: 
* Too many neurons
* Not enough data 
* Bad network 

To cure overfitting: 
* Dropout (note: some noise may come back. Not recommended with conv nets.)
* Data augmentation(add noise to data) 

###### Batch normalization 
Data in real world: large values, different scales, skewed, correlated

Solution:

1. Data whitening:
   * Scale: center around zero 
   * Decorrelate: (A+B)/2, A-B (PCA etc) 
   * Add an additional layer and let NN do it (to determine what the clean data is)

2. Batch normalization (better option) 
   * Works better than whitening 
   * Usually insterted after a FC/CL and a non linerity: .. FC -> BN -> Tanh -> FC -> BN -> Tanh -> ..
   * How to: 
![Batch Normalization](https://raw.githubusercontent.com/spartonia/MLNotes/master/static/batchNormalization.png "Batch Normalization done right")

Note: 
* with batch normalization, bete replace bias so don't use bias when batch normalizing. 
* you can use higher lrate 
* stop using (or do a little) dropout 

#### Ensamble
* Ensambling independant models increases the accuracy ~2% 
* You can also ensamble saved checkpoints of a model

# Choosing a Deep Learning library
* Feature extracting / fine tuning existing network: **Caffe** 
* Cpmplex uses of pretrained models: **Lassagne** or **Torch**
* Write your own layers: **Torch** 
* Crazy RNNs: **Theano** or **Tensorflow** 
* Huge model, need parallelism: **Tensorflow** 


# Useful links
* [Must Know Tips/Tricks in Deep Neural Networks ](http://lamda.nju.edu.cn/weixs/project/CNNTricks/CNNTricks.html)
