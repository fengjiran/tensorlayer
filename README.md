<!--<div align="center">
	<div class="TensorFlow">
  <img src="https://www.tensorflow.org/images/tf_logo_transp.png" style=": left; margin-left: 5px; margin-bottom: 5px;"><br><br>
   </div>
   <div class="TensorLayer">
    <img src="https://www.tensorflow.org/images/tf_logo_transp.png" style=": right; margin-left: 5px; margin-bottom: 5px;">
    </div>
</div>
-->
<a href="http://tensorlayer.readthedocs.io">
<div align="center">
	<img src="img/img_tensorlayer.png" width="30%" height="30%"/>
</div>
</a>

[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/tensorlayer/Lobby#?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

TensorLayer is a deep learning and reinforcement learning library based on [Google TensorFlow](https://www.tensorflow.org). It provides rich data processing, model training and serving modules to help researchers and engineers build practical machine learning workflows.  

# What's New
* Release [Sub-pixel Convolution 1D](http://tensorlayer.readthedocs.io/en/latest/modules/layers.html#d-supixel-convolutional) for Audio Super-resolution.
* Release [Flickr dataset loader](http://press.liacs.nl/mirflickr/mirdownload.html), see [load_flickr25k](http://tensorlayer.readthedocs.io/en/latest/modules/files.html#flickr25k) and [load_flickr1M](http://tensorlayer.readthedocs.io/en/latest/modules/files.html#flickr1m).
* Release [SpatialTransformer2dAffineLayer](http://tensorlayer.readthedocs.io/en/latest/modules/layers.html#spatial-transformer) for [Spatial Transformer Networks](https://github.com/zsdonghao/Spatial-Transformer-Nets) see [example code](https://github.com/zsdonghao/Spatial-Transformer-Nets).
* Release [Sub-pixel Convolution 2D](http://tensorlayer.readthedocs.io/en/latest/modules/layers.html#super-resolution-layer) for Super-resolution see [SRGAN code](https://github.com/zsdonghao/SRGAN).
* Join [Slack](https://join.slack.com/t/tensorlayer/shared_invite/MjExMjMzODAwNjI0LTE0OTk4ODEzMjUtNmVjNjQ4ZjMzMw) Now.
* [Attention Seq2seq](https://github.com/zsdonghao/tensorlayer/issues/164) help wanted.
* You can now use TensorLayer with [TF-Slim](http://tensorlayer.readthedocs.io/en/latest/modules/layers.html#connect-tf-slim) and [Keras](http://tensorlayer.readthedocs.io/en/latest/modules/layers.html#connect-keras) together!

# Design Philosophy

As deep learning practitioners, we have been looking for a library that can serve for various development phases. This library shall be easy for beginners by providing rich neural network reference implementations. Later, it can be extended to address real-world problems by controlling training backends to exhibit low-level cognitive behaviours. In the end, it shall be able to serve in challenging production environments.

TensorLayer is designed for beginning, intermediate and professional deep learning users with following goals:

- *Simplicity* : TensorLayer lifts the low-level dataflow abstraction of TensorFlow to high-level deep learning modules. 
A user often find it easy to bootstrap with TensorLayer, and then dive into low-level implementation only if need. 
- *Transparency* : TensorLayer provides access to the native APIs of TensorFlow. This helps users achieve flexible controls within the training engine.
- *Composability* : If possible, deep learning modules are composed, not built. TensorLayer can glue existing pieces together (e.g., connected with [TF-Slim](http://tensorlayer.readthedocs.io/en/latest/modules/layers.html#connect-tf-slim) and [Keras](http://tensorlayer.readthedocs.io/en/latest/modules/layers.html#connect-keras)).
- *Performance* : TensorLayer provides zero-cost compatibility for TensorFlow. It can run on distributed yet heterogeneous platforms.

# Why TensorLayer

A frequent question regarding TensorLayer is that why don't we use libraries like Keras and Tflearn. 
These libraries are comfortable to start with. They provide imperative abstractions to lower adoption barrier; 
but in turn mask the underlying engine from users. Though good for bootstrap, 
it becomes hard to tune and modify from the bottom, which is quite necessary in tackling many real-world problems. 

Without compromise in simplicity, TensorLayer advocates a more flexible and composable paradigm: 
neural network libraries shall be used interchangeably with the native engine. 
This allows users to enjoy the ease of pre-built modules without losing visibility to the deep. 
This non-intrusive nature also makes it viable to consolidate with other TF's wrappers such as TF-Slim and Keras. 
However, flexibility does not sacrifice performance. TensorLayer allows seamless distributed and heterogeneous deployment.

TensorLayer is in an active development stage and has received numerous contributions from an open community. 
It has been widely used by researchers from Imperial College London, Carnegie Mellon University, Stanford University, 
Tsinghua University, UCLA, Linköping University and etc., 
as well as engineers from Google, Microsoft, Alibaba, Tencent, ReFULE4, Bloomberg and many others.


# Installation

TensorLayer has install prerequisites including TensorFlow, numpy and matplotlib. For GPU support, CUDA and cuDNN are required. Please check [here](http://tensorlayer.readthedocs.io/en/latest/user/installation.html) for detailed instructions.

If you already had the pre-requisites ready (numpy, scipy, scikit-image, matplotlib and nltk(optional)), the simplest way to install TensorLayer in your python program is: 

```bash
[for master version] pip install git+https://github.com/zsdonghao/tensorlayer.git (Highly Recommended)
[for stable version] pip install tensorlayer
```

# Documentation

The documentation [[Online]](http://tensorlayer.readthedocs.io/en/latest/) [[PDF]](https://media.readthedocs.org/pdf/tensorlayer/latest/tensorlayer.pdf) [[Epub]](http://readthedocs.org/projects/tensorlayer/downloads/epub/latest/) [[HTML]](http://readthedocs.org/projects/tensorlayer/downloads/htmlzip/latest/) describes the usages of TensorLayer APIs. It is also a self-contained document that walks through different types of deep neural networks, reinforcement learning and their applications in Natural Language Processing (NLP) problems. 

We have included the corresponding modularized implementations of Google TensorFlow Deep Learning tutorial, so you can read the TensorFlow tutorial [[en]](https://www.tensorflow.org/versions/master/tutorials/index.html) [[cn]](http://wiki.jikexueyuan.com/project/tensorflow-zh/) along with our document.

[Chinese documentation](http://tensorlayercn.readthedocs.io/zh/latest/) is also available.

# Your First Program

The first program trains a multi-layer perception network to solve the MNIST problem. We use the well-known  [scikit](http://scikit-learn.org/stable/)-style functions such as ``fit()`` and ``test()``. The program is self-explained.

```python
import tensorflow as tf
import tensorlayer as tl

sess = tf.InteractiveSession()

# Prepare data
X_train, y_train, X_val, y_val, X_test, y_test = tl.files.load_mnist_dataset(shape=(-1,784))

# Define placeholder
x = tf.placeholder(tf.float32, shape=[None, 784], name='x')
y_ = tf.placeholder(tf.int64, shape=[None, ], name='y_')

# Define the neural network structure
network = tl.layers.InputLayer(x, name='input')
network = tl.layers.DropoutLayer(network, keep=0.8, name='drop1')
network = tl.layers.DenseLayer(network, 800, tf.nn.relu, name='relu1')
network = tl.layers.DropoutLayer(network, keep=0.5, name='drop2')
network = tl.layers.DenseLayer(network, 800, tf.nn.relu, name='relu2')
network = tl.layers.DropoutLayer(network, keep=0.5, name='drop3')

# The softmax is implemented internally in tl.cost.cross_entropy(y, y_) to
# speed up computation, so we use identity here.
# see tf.nn.sparse_softmax_cross_entropy_with_logits()
network = tl.layers.DenseLayer(network, n_units=10, act=tf.identity, name='output')
                                
# Define cost function and metric.
y = network.outputs
cost = tl.cost.cross_entropy(y, y_, 'cost')
correct_prediction = tf.equal(tf.argmax(y, 1), y_)
acc = tf.reduce_mean(tf.cast(correct_prediction, tf.float32))
y_op = tf.argmax(tf.nn.softmax(y), 1)

# Define the optimizer
train_params = network.all_params
train_op = tf.train.AdamOptimizer(learning_rate=0.0001).minimize(cost, var_list=train_params)

# Initialize all variables in the session
tl.layers.initialize_global_variables(sess)

# Print network information
network.print_params()
network.print_layers()

# Train the network, we recommend to use tl.iterate.minibatches()
tl.utils.fit(sess, network, train_op, cost, X_train, y_train, x, y_,
            acc=acc, batch_size=500, n_epoch=500, print_freq=5,
            X_val=X_val, y_val=y_val, eval_train=False)

# Evaluation
tl.utils.test(sess, network, acc, X_test, y_test, x, y_, batch_size=None, cost=cost)

# Save the network to .npz file
tl.files.save_npz(network.all_params , name='model.npz')

sess.close()
```

We provide many helper functions (like `fit()` , `test()`) that is similar to Keras to facilitate your development; however, if you want to obtain a fine-grain control over the model or its training process, you can use TensorFlow’s methods like `sess.run()` in your program directly (`tutorial_mnist.py` provides more details about this). Many more DL and RL examples can be found [here](http://tensorlayer.readthedocs.io/en/latest/user/example.html).

[Tricks to use TL](https://github.com/wagamamaz/tensorlayer-tricks) is also a good introduction to use TensorLayer.



# Examples

Examples can be found [in this repository](https://github.com/zsdonghao/tensorlayer/tree/master/example) and [TensorLayer Topic](https://github.com/search?q=topic%3Atensorlayer&type=Repositories).

## Basics
 - Multi-layer perceptron (MNIST). A multi-layer perceptron implementation for MNIST classification task, see [tutorial\_mnist\_simple.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_mnist_simple.py).
 - Multi-layer perceptron (MNIST) classification using Iterator, see [method1](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_mlp_dropout1.py) and [method2](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_mlp_dropout2.py).


## Computer Vision
 - Denoising Autoencoder (MNIST). A multi-layer perceptron implementation for MNIST classification task, see [tutorial_mnist.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_mnist.py).
 - Stacked Denoising Autoencoder and Fine-Tuning (MNIST). A multi-layer perceptron implementation for MNIST classification task, see [tutorial_mnist.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_mnist.py).
 - Convolutional Network (MNIST). A Convolutional neural network implementation for classifying MNIST dataset, see [tutorial_mnist.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_mnist.py).
 - Convolutional Network (CIFAR-10). A Convolutional neural network implementation for classifying CIFAR-10 dataset, see [tutorial\_cifar10.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_cifar10.py) and [tutorial\_cifar10_tfrecord.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_cifar10_tfrecord.py).
 - VGG 16 (ImageNet). A Convolutional neural network implementation for classifying ImageNet dataset, see [tutorial_vgg16.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_vgg16.py).
 - VGG 19 (ImageNet). A Convolutional neural network implementation for classifying ImageNet dataset, see [tutorial_vgg19.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_vgg19.py).
 - InceptionV3 (ImageNet). A Convolutional neural network implementation for classifying ImageNet dataset, see [tutorial\_inceptionV3_tfslim.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_inceptionV3_tfslim.py).
 - Wide ResNet (CIFAR) by [ritchieng](https://github.com/ritchieng/wideresnet-tensorlayer).
 - More CNN implementations of [TF-Slim](https://github.com/tensorflow/models/tree/master/slim#pre-trained-models) can be connected to TensorLayer via SlimNetsLayer.
 - [Spatial Transformer Networks](https://arxiv.org/abs/1506.02025) by [zsdonghao](https://github.com/zsdonghao/Spatial-Transformer-Nets).
 - [U-Net for brain tumor segmentation](https://github.com/zsdonghao/u-net-brain-tumor) by [zsdonghao](https://github.com/zsdonghao/u-net-brain-tumor).
 - Variational Autoencoder (VAE) for CelebA by [yzwxx](https://github.com/yzwxx/vae-celebA).

## Natural Language Processing
 - Recurrent Neural Network (LSTM). Apply multiple LSTM to PTB dataset for language modeling, see [tutorial_ptb_lstm.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_ptb_lstm.py) and [tutorial\_ptb\_lstm\_state\_is_tuple.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_ptb_lstm_state_is_tuple.py).
 - Word Embedding - Word2vec. Train a word embedding matrix, see [tutorial\_word2vec_basic.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial\_word2vec_basic.py).
 - Restore Embedding matrix. Restore a pre-train embedding matrix, see [tutorial\_generate_text.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_generate_text.py).
 - Text Generation. Generates new text scripts, using LSTM network, see [tutorial\_generate_text.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_generate_text.py).
 - Chinese Text Anti-Spam by [pakrchen](https://github.com/pakrchen/text-antispam).

## Adversarial Learning
- DCGAN - Generating images by [Deep Convolutional Generative Adversarial Networks](http://arxiv.org/abs/1511.06434) by [zsdonghao](https://github.com/zsdonghao/dcgan).
- [Generative Adversarial Text to Image Synthesis](https://github.com/zsdonghao/text-to-image) by [zsdonghao](https://github.com/zsdonghao/text-to-image).
- [Unsupervised Image to Image Translation with Generative Adversarial Networks](https://github.com/zsdonghao/Unsup-Im2Im) by [zsdonghao](https://github.com/zsdonghao/Unsup-Im2Im).
- [Super Resolution GAN](https://arxiv.org/abs/1609.04802) by [zsdonghao](https://github.com/zsdonghao/SRGAN).

## Reinforcement Learning
 - Policy Gradient / Network - Atari Ping Pong, see [tutorial\_atari_pong.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_atari_pong.py).
 - Deep Q-Network - Frozen lake, see [tutorial\_frozenlake_dqn.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_frozenlake_dqn.py).
 - Q-Table learning algorithm - Frozen lake, see [tutorial\_frozenlake\_q_table.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_frozenlake_q_table.py).
 - Asynchronous Policy Gradient using TensorDB - Atari Ping Pong by [nebulaV](https://github.com/akaraspt/tl_paper).
 - AC for discrete action space - Cartpole, see [tutorial\_cartpole_ac.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_cartpole_ac.py).
 - A3C for continuous action space - Bipedal Walker, see [tutorial\_bipedalwalker_a3c*.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_bipedalwalker_a3c_continuous_action.py).
 - [DAGGER](https://www.cs.cmu.edu/%7Esross1/publications/Ross-AIStats11-NoRegret.pdf) - [Gym Torcs](https://github.com/ugo-nama-kun/gym_torcs) by [zsdonghao](https://github.com/zsdonghao/Imitation-Learning-Dagger-Torcs).
 - [TRPO](https://arxiv.org/abs/1502.05477) for continuous and discrete action space by [jjkke88](https://github.com/jjkke88/RL_toolbox).

## Applications
- Image Captioning - Reimplementation of Google's [im2txt](https://github.com/tensorflow/models/tree/master/im2txt) by [zsdonghao](https://github.com/zsdonghao/Image-Captioning).
- A simple web service - [TensorFlask](https://github.com/JoelKronander/TensorFlask) by [JoelKronander](https://github.com/JoelKronander).

## Special Examples
 - Merge TF-Slim into TensorLayer. [tutorial\_inceptionV3_tfslim.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_inceptionV3_tfslim.py).
 - Merge Keras into TensorLayer. [tutorial_keras.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_keras.py).
 - Data augmentation with TFRecord. Effective way to load and pre-process data, see [tutorial_tfrecord*.py](https://github.com/zsdonghao/tensorlayer/tree/master/example) and [tutorial\_cifar10_tfrecord.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_cifar10_tfrecord.py).
 - Data augmentation with TensorLayer, see [tutorial\_image_preprocess.py](https://github.com/zsdonghao/tensorlayer/blob/master/example/tutorial_image_preprocess.py).
 - TensorDB by [fangde](https://github.com/fangde) see [here](https://github.com/akaraspt/tl_paper).

## Notes
* TensorLayer provides two set of Convolutional layer APIs, see [(Professional)](http://tensorlayer.readthedocs.io/en/latest/modules/layers.html#convolutional-layer-pro) and [(Simplified)](http://tensorlayer.readthedocs.io/en/latest/modules/layers.html#convolutional-layer-simplified) on readthedocs website.
* If you get into trouble, you can start a discussion on [Slack](https://join.slack.com/t/tensorlayer/shared_invite/MjExMjMzODAwNjI0LTE0OTk4ODEzMjUtNmVjNjQ4ZjMzMw), [Gitter](https://gitter.im/tensorlayer/Lobby#?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge>),
[Help Wanted Issues](https://waffle.io/zsdonghao/tensorlayer),
[QQ group](https://github.com/zsdonghao/tensorlayer/blob/master/img/img_qq.png) and [Wechat group](https://github.com/shorxp/tensorlayer-chinese/blob/master/docs/wechat_group.md).


# License

TensorLayer is released under the Apache 2.0 license.

# Contributions

TensorLayer is maintained by numerous Github contributors [here](https://github.com/zsdonghao/tensorlayer/graphs/contributors).

<!--
TensorLayer started as an internal repository at Imperial College London, helping researchers to test their new methods. It now encourages researchers from all over the world to controbute their methods so as to promote the development of machine learning. You can either contact us to discuss your ideas, or fork our repository and make a pull request.
 -->

- 🇬🇧 If you are in London, we can discuss in person. Drop us an email to organize a meetup: tensorlayer@gmail.com.
- 🇨🇳 我们有官方的 [中文文档](http://tensorlayercn.readthedocs.io/zh/latest)。另外, 我们建立了多种交流渠道，如[QQ群](img/img_qq.png)和[微信群](https://github.com/shorxp/tensorlayer-chinese/blob/master/docs/wechat_group.md).

# Citation
If you find it is useful, please cite our paper in your project and paper.

```
@article{TensorLayer2017,
author = {Dong, Hao and Supratak, Akara and Mai, Luo and Liu, Fangde and Oehmichen, Axel and Yu, Simiao and Guo, Yike},
journal = {ACM Multimedia},
title = {{TensorLayer: A Versatile Library for Efficient Deep Learning Development}},
url = {http://tensorlayer.org},
year = {2017}
}
```
