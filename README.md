# Image-Retrieval-Representation-learning

In an image retrieval task, there are two fundamental units: image repository, and query image. Simply put, an image repository is a collection of images. A query image is a reference used to retrieve other images from the repository that are perceptually close to it. Image retrieval's task is to rank images in an index set with respect to their relevance to a query image.

![Image retrieval](/assets/img_retrieval.png)

Here I will demonstarte two differen ways of trainnig an unsupervised 
In this project, I will demonstrate the image retrieval problem from an unsupervised perspective. The foundation of the work lies in the latent space representation of the images learned through a self-supervised learning task. The goal here is to capture the latent space embeddings of images and then try to determine the distance among them in the latent space. Then we identify the issues in learning in a purely unsupervised scenario (link) and show the enhancement in the information content of the learned representations with a hint of supervision. We train a regularised autoencoder with the supervised information. We validate the performance in a retrieval framework for the test set.

Training data used: [CIFAR 10](https://www.cs.toronto.edu/~kriz/cifar-10-python.tar.gz)

Labels required: No

Loss function: Mean squared error(MSE)

Neural network architecture: Encoder-Decoder network

Performance evaluation metrics: normalized mutual information score & rand index

### Method:

![nn-architecture](/assets/encoder-decoder.png)


