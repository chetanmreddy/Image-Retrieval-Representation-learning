# Image-Retrieval-Representation-learning

In an image retrieval task, there are two fundamental units: image repository, and query image. Simply put, an image repository is a collection of images. A query image is a reference used to retrieve other images from the repository that are perceptually close to it. Image retrieval's task is to rank images in an index set with respect to their relevance to a query image.

![Image retrieval](/assests/img_retrieval.png)

 
In this project, I will demonstrate the image retrieval problem from an unsupervised perspective. The foundation of the work lies in the latent space representation of the images learned through a self-supervised learning task. The goal here is to capture the latent space embeddings of images and then try to determine the distance among them in the latent space. Then I identify the issues in learning in a purely unsupervised scenario and show the enhancement in the information content of the learned representations with a supervision head. I train a regularised autoencoder with the supervised information. We validate the performance in a retrieval framework for the test set.

Training data used: [CIFAR 10](https://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz)

Labels required: No

Loss function: Mean squared error(MSE)

Neural network architecture: Encoder-Decoder network

Performance evaluation metrics: normalized mutual information score & rand index

### Method1:

![nn-architecture](/assests/encoder-decoder.png)

In the training phase, I use autoencoders to compress high dimensional image representation to latent space embedding. These embeddings can be thought of as points in the latent space. These embeddings are then clustered together by the k-means algorithm. After training, we have a repository of embeddings that are clustered in the latent space.

### Training curves:

![train loss curve](/assests/train-loss1.png)

The self-supervised loss is logged and one can see that the training and validation loss went down. This signifies than the latent space has indeed learned the image representations and can be used to construct images back. The plot also signifies the convergence of the self-supervised loss function.

The training was performed for a mere 10 epochs. The validation data is 20\% of the training data used.

![tsne](/assests/tsne1.png)

The plot above shows the t-SNE of the embeddings. There are 10 colors each for the 10 classes. We can see that points of the same colors do clutter together but not that much to be prominent.

Test Images:
![](/assests/reconstruction1.png)

Reconstruction of Test images:
![](/assests/reconstruction1_res.png)


![](/assests/query1.png)




### Method2:
In this method, the autoencoder remains the same. That is to say, the architecture and the configuration are the same. The only change that is made is an addition of a classification head to the bottleneck(end of encoder).

Test Images:
![](/assests/reconstruction2.png)

Reconstruction of Test images:
![](/assests/reconstruction2_res.png)

The reconstructions are not that good as with a vanilla autoencoder. This means that the classification head is interfering with the embeddings. Come to think of it, both the objectives (reconstruction and classification) are fighting against each other in the process. This leads to a more inferior reconstruction but a better latent space alignment, as is shown below in the report.


![tsne](/assests/tsne2.png)

Due to the classification task, the embeddings are far better clustered. This means that not only do the embeddings represent the images but also now know which image belongs to which class.

![](/assests/query2.png)

### The Evaluation on the Clustering

Models	                   |  NMI                      | RI
:-------------------------:|:-------------------------:|:------------------------:
Vanilla Autoencoder        |  0.074                    |0.811
Autoencoder with classification head|0.433             |0.876

The NMI and RI seem to increase significantly with the addition of the classification head. This also directs us towards the fact that the representation learned is much more informative and has the contextual information in the second case.






