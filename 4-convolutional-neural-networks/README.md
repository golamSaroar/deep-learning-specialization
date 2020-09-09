## Convolutional Neural Networks

![vertical-edge-detection](slides/1-vertical-edge-detection.png)

![vertical-edge-detection-example](slides/2-vertical-edge-detection-examples.png)

If you take a six by six image and convolve it with a three by three filter, you end up with a four by four output with a four by four matrix, and that's because there are only four by four possible positions, for the three by three filter to fit in your six by six matrix. The formula is:  
`n x n *conv f x f => n-f+1 x n-f+1`

What are the downsides to this:
- Shrinking output
- Throwing away information from edges (as the pixels at the edges are used in only one of the outputs) 

In order to solve both of these problems, add padding to the image. If you add 1 pixel at each side, the 6x6 image becomes 8x8 and we get 8x8 *conv 3x3 => 6x6. The formula is:  
`n x n *conv f x f => n+2p-f+1 x n+2p-f+1`  
where n=6, f=3, and p = 1 in our example.

**Same convolution**: Pad so that output size is the same as the input size.  
`n+2p-f+1 x n+2p-f+1`  
`n+2p-f+1 = n when`  
`p = (f-1)/2; by convention, f is usually odd`

![3-strided-convolution](slides/3-strided-convolution.png)

![4-multiple-filters](slides/4-multiple-filters.png)

![5-example-of-a-layer](slides/5-example-of-a-layer.png)

CNN is less prone to overfitting because once the network learns N feature detectors that work, it can be applied even to larger images. And the number of parameters will be fixed and small. For example, if you have 10 filters that are 3x3x3 in one layer of a NN, that layer has 27*10+10= 280 parameters. This is true for images of dim 40x40, also 1000x1000.

![6-summary-of-notation](slides/6-summary-of-notation.png)

![7-example-convnet](slides/7-example-convnet.png)

As you go deeper in a neural network, typically you start off with larger images, 39 by 39. And then the height and width will stay the same for a while and gradually trend down as you go deeper in the neural network. It's gone from 39 to 37 to 17 to 7. Whereas the number of channels will generally increase. It's gone from 3 to 10 to 20 to 40, and you see this general trend in a lot of other convolutional neural networks as well.

![8-max-pooling](slides/8-max-pooling.png)

![9-average-pooling](slides/9-average-pooling.png)

Average pooling is rarely used. Max pooling with f=2, s=2 (a factor of 2) is more common. Also, padding is almost never used in pooling. 

In pooling, there are no parameters to learn.

![10-nn-example](slides/10-nn-example.png)

### Why Convolutions?

- **parameter sharing**: a feature detector (such as a vertical edge detector) that’s useful in one part of the image is probably useful in another part of the image.   
- **sparsity of connections**: in each layer, each output value depends only on a small number of inputs.

### CNN Case Studies

![11-lenet5](slides/11-lenet5.png)

![12-alexnet](slides/12-alexnet.png)

![13-vgg16](slides/13-vgg16.png)

![14-residual-block](slides/14-residual-block.png)

![15-residual-network](slides/15-residual-network.png)

**Why ResNets Work**: Did not understand the “identity function” bit, will have to come back to this later. 

![16-1x1-conv](slides/16-1x1-conv.png)

Some use-cases of a 1x1 Convolution:   
- adds non-linearity and therefore, allows you to learn the more complex function of your network
- shrink the number of channels and therefore, save on computation in some networks

![17-inception-network-motivation](slides/17-inception-network-motivation.png)

![18-computational-cost-problem](slides/18-computational-cost-problem.png)

![19-1x1-conv-solution](slides/19-1x1-conv-solution.png)

![20-inception-module](slides/20-inception-module.png)

![21-inception-network](slides/21-inception-network.png)

**Need to learn more about the Inception network.**

![22-transfer-learning](slides/22-transfer-learning.png)

The above diagram explains three scenarios.

In the first case, we have a small dataset. So, we download an open source implementation- not just the code but also the weights- then get rid of the softmax layer and create our own softmax unit that outputs our target variables. We should think of all of these layers as frozen so we freeze the parameters in all of these layers of the network and then just train the parameters associated with our softmax layer.

In the second case, we have a larger labeled dataset, therefore, we should freeze fewer layers. Although if the output layer has different clauses, then we need to have our own output unit. There are a couple of ways to do this. We could take the last few layers’ weights and just use that as initialization and do gradient descent from there or we can also blow away these last few layers and just use our own new hidden units to get our own final softmax outputs.

In the third and last case, we have a lot of data, so we take this open source network and weights and use the whole thing just as initialization and train the whole network. Although again we need our own softmax output- the output of labels we care about.

Computer vision is one discipline where transfer learning is something that **we should almost always do** unless we have an exceptionally large dataset to train everything else from scratch ourself.

### Object Detection

![23-sliding-windows](slides/23-sliding-windows.png)

![24-yolo-algo](slides/24-yolo-algo.png)

![25-object-localization](slides/25-object-localization.png)

![26-nonmax-suppression](slides/26-nonmax-suppression.png)

![27-anchor-box-algo](slides/27-anchor-box-algo.png)

![28-anchor-box-example](slides/28-anchor-box-example.png)

### Face Detection

![29-similarity-function](slides/29-similarity-function.png)

#### Siamese Network

![30-siamese-network](slides/30-siamese-network.png)

#### Triplet Loss

![31-learning-objective](slides/31-learning-objective.png)

![32-choosing-the-triplets](slides/32-choosing-the-triplets.png)

#### Neural Style Transfer

![33-neural-style-transfer](slides/33-neural-style-transfer.png)

![34-content-cost-function](slides/34-content-cost-function.png)

`l` was chosen to be somewhere in the middle of the layers of the neural network, neither too shallow nor too deep.
