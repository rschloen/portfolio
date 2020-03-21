---
layout: post
title:  "Surface EMG Control for a Robotic Hand"
featured-img: demo_thumb
date:   2020-01-10 14:46:01 -0600
---

# Surface Electromyography control for a Robotic Hand

The goal of this project was to achieve accurate, real time prediction of hand gestures using surface electromyography (SEMG) and deep learning with transfer learning. Transfer learning is the concept of using the relationships learned from one problem on a similar problem. In this case, I am using transfer learning to take the relationships learned from one data set of EMG recordings and applying it to a new smaller data set to reduce the training time and effort. Using this method, a model more specific to an individual can be quickly trained from a relatively small amount of data.

<iframe width="560" height="315" src="https://www.youtube.com/embed/uckYHXjnjIc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### Data Acquisition

Deep learning requires a lot of data in order to accurately learn the relationships between the inputs and the outputs. I used the Ninapro [1] online database of EMG recordings as the bulk of the data to train my neural network. The Ninapro database that I used uses the same acquisition system to record the data that I used for this project. That was Thalmic Labs' Myo Armband, which provides 8 channels of EMG data from the 8 electrodes in the armband.

<!-- <img src="{{ site.url }}{{site.baseurl}}/assets/img/post/myo-front-view.jpg" alt="Myo Armband"/> -->
![Myo Armband](https://github.com/rschloen/portfolio/tree/master/assets/img/posts/myo-front-view.jpg)
* Myo Armband (*Photo Credit: Thalmic labs*)

### Convolutional Neural Networks (CNN)

The type of neural network I chose to use for this project was a convolutional neural network (CNN). Convolutional neural networks are a type of deep learning that are commonly used to classify images. The convolutional layers pass a kernel, or filter, over the image and extract a feature map representing an abstract or lower level feature (such as lines on your face) within the image. After passing through multiple convolutional layers, these features are then connected to fully connected, or dense, layers and the relationships between the now connected features are learned and used to classify the image. For this project, the image is a interval of EMG data that is 260 ms long equaling 52 samples since the Myo Armband has a sample rate of 200 Hz. With 52 samples, with 8 values per sample, you now have a 52 by 8 by 1 (height, length, depth) image that you can pass through the network.

![Example CNN](https://github.com/rschloen/portfolio/tree/master/assets/img/posts/sample_CNN.png)
* Diagram of enhanced CNN architecture from [3] which I adapted to create the final CNN


### Training and Hyperparameter Tuning

To train the network, the dataset was split into training, validation, and testing sets, where each sample in the sets consists of an input and a label. The training consisted of running a number of epochs, which is where you pass all of your training data through your model and update the model based on how well it performed; that is, whether the output of the model matched the label that came with the input. After you run a training epoch, you then run a validation epoch, where you pass all the validation data through your model to see how well it is performing on data it has not seen before. The model is not updated during validation. Once the desired number of epochs has been completed, or your model is not improving anymore, a final testing epoch is run to evaluate how well the fully trained model performs on never before seen data.

Using this training loop, the hyperparameters, the values and functions set before training begins, can be tuned. An example of a common hyperparameter is the learning rate for the optimizer that updates the model. By looping through a number of models with different potential learning rates and evaluating the models, the best learning can be found. Using this idea, I tuned the hyperparameters for my network in order to achieve the best performance.

![Example data](https://github.com/rschloen/portfolio/tree/master/assets/img/posts/emg_gesture_id_1cycle.png)
* Sample of 8 channel EMG data and corresponding label

To learn more about this project, visit this project's [Github repository](https://github.com/rschloen/semg_control).


*Photo Credit: Open Bionics*
