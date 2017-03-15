A Convolution layer
* Accepts a volume f size `W1 x H1 x D1`
* Requires four hyper parameters
   * Number of filters `K` (powers of 2 is common)
   * their spatial extent `F` (filter size)
   * the stride `S` 
   * zero padding  `P`
   * commoc settings: (F, S, P): (3,1,1), (5,1,2), (5,2,?), (1,1,0)
* Produces volume of `W2 x H2 x D2` 
   * `W2 = (W1 - F + 2P)/S + 1`
   * `H2 = (H2 - F + 2P)/S + 1`
   * `D2 = K`
   
Tips/Tricks
-----------
* GoogLeNet removed the final FC layers (which are the most memory-heavy parts). One way to reduce the number/size of FC layers is that use the average of final Conv filters instead of using all cells. For instance, if you have a final conv layer of `7x7x256`, you can avergave them to `1x256` (`7x7` size of each filter) and connect it to a FC layer. 
* Trend towards smaller filters and deeper architectures 
* Typical architecture
   * `[(conv-relu)xN-pool?]xM-(FC-relu)xK,softmax` where `N~=5`, `M` is large, `0<=K<=2`.
   * But ResNet/GoogLeNet challenge this paradigm.
   
**Data Augmentation**
Is simple to use, use it. 
   * Horizontal flip 
   * Random crops (a patch and resize)
      * Note: During test time, use a subset of these crops to calculate the loss instead of using the (whole) original image. 
   * Color jittering (change the colors a bit). There is a recommended way to do it using PCA. 
   * Get creative
      * Translation
      * Rotations
      * Streching 
      * Shearing
      * etc 
 
A genaral theme: 
   * **Training:** Add random noise 
   * **Testing:** Marginalize over random noise 
   
** Transfer Learning**
Main advantage: You dont need many data to train CNNs 
1. Take and download a favorite CNN architecture
2. Depending on the size of your dataset, pick some layers on top. 
![Transfer Learning](https://raw.githubusercontent.com/spartonia/MLNotes/master/static/transferLearning.png "Transfer learning guide.")
      
   
