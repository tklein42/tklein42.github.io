---
title:  "Deep Learning Simulator"
mathjax: true
layout: post
categories: media
---
With the modern world being taken aback by the recent advancements in artificial intelligence, particularly deep learning, the global desire to learn more about these topics has also increased. Although people can find no shortage of literature to learn about all the complexities that go into the field, this can be an intimidating mountain to climb, especially for those with little to no experience in topics such as programming, statistics, linear algebra, algorithms, and data structures. This project aims to serve as the educational gateway for those who may be ill-prepared to tackle the core of deep learning but still want to explore the field and understand how these problems are structured.


## Functionality

As previously mentioned, this tool aims to open the average person to the realm of deep learning principles, leveraging PyTorch's Libtorch C++ API as a foundational tool, alongside an interactive interface put together utilizing OpenGL. It aims to provide a hands-on, accessible approach for enthusiasts and learners eager to delve into the depths of machine learning using a robust open-source framework. The interface itself offers the user an easy-to-use drag-and-drop layer visualization, where the user can simply drag two desired layers close to one another and snap them together. This allows users to see the current size of the model and how deep the current architecture is. As this is the first version of the proposed simulator, currently the user only is capable of utilizing linear and convolutional layers, due to the MNIST classification dataset being the only data available to experiment with. When in the layer visualization, however, there are several features within each layer that the user is capable of editing and also can append additional operations to occur after the selected layer. Some of the current features are as follows:

* Input:
  * Number of the input features the layer is expected from the previous layer
* Output:
  * Number of the output features the layer is expected to output to the next layer
* Dropout:
  * Percentage of output features that are "dropped" (set to zero). Which is a regularization technique.
* Max Pooling (Conv):
  * Calculates the maximum value for 2x2 patches within the convolutional feature maps, effectively reducing the size by a factor of 2
* Kernel Size (Conv):
  * Refers to the size of the filters that are applied to each channel of the previous input.
 
Alongside these features for editing layers, when the user has decided they would like to test the model's performance they can select a run button where more options for training can be selected. These options include:

* Optimizer:
  * Allows choice of optimizers, which are algorithms used in training that enable models to learn.
* Initial Learning Rate:
  * Allows the user to set the initial learning rate for training to occur.
* Learning Rate Scheduler:
  * Allows the user to set up a learning rate scheduler that decreases the learning rate after a certain condition is met or after a certain number of epochs.
* Epochs:
  * Allows the user to choose the number of epochs to train for, which is the number of times the model gets to see the dataset and learn from it.
 
Once the user selects the desired configuration of the run, the interface allows for real-time viewing of performance charts such as accuracy and loss while the model is being trained in the background. This allows the user to identify early trends in the performance and if they so desire they are capable of stopping the training and return to the layer visualization page where they can make any adjustments they see fit. 

Through this project, users gain exposure to practical implementations of fundamental deep learning concepts. It accomplishes this by allowing the user to be in charge of the end-to-end pipeline and learn each of the different components making up a deep learning pipeline by conducting their very own ablation studies to learn how each component affects the results. By advocating for open-source tools like PyTorch's Libtorch C++ API, this project aims to democratize the learning curve associated with deep learning. It underscores the significance of accessible resources and tools in enabling aspiring developers and enthusiasts to comprehend and implement sophisticated machine learning models, fostering a community of knowledge sharing and collaborative learning.

![Interface](/assets/dl_simulator/interface.jpg)
