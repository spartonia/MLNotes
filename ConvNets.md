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
