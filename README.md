# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/example_of_classes.png ""
[image2]: ./examples/number_of_raining_set_per_class.png ""
[image3]: ./examples/example_of_original_image.png "Random Noise"
[image4]: ./examples/example_of_normalized_image.png "Traffic Sign 1"
[image5]: ./test_examples/1x.png "Traffic Sign 2"
[image6]: ./test_examples/2x.png "Traffic Sign 3"
[image7]: ./test_examples/3x.png "Traffic Sign 4"
[image8]: ./test_examples/5x.png "Traffic Sign 5"
[image9]: ./test_examples/6x.png "Traffic Sign 5"
[image10]: ./test_examples/8x.png "Traffic Sign 5"
[image11]: ./test_examples/9x.png "Traffic Sign 5"
[image12]: ./test_examples/stop.png "Traffic Sign 5"
[image13]: ./examples/test_on_eight_images.png "Traffic Sign 5"
[image14]: ./examples/eight_images_softmax.png "Traffic Sign 5"
[image15]: ./examples/visualize_nn.png "Traffic Sign 5"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/ozdemre/SDC-NanoDegree-Project3-Traffic-Sign-Classifier/blob/main/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the numpy library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is 32x32x3
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. After loading the data, first I plotted the first picture of each class.


![alt text][image1]

Then I plotted number of training data per each class to see the training data distribution.

![alt text][image2]


### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

For pre processing the images, I decided to convert the images to grayscale and normalize around zero.

![alt text][image3]![alt text][image4]


This step is particularly important for optimizer since optimizer numerically works more stable around mean zero value.


To increase the accuracy of the model some augmentation techniques can also be used. (such as: transforms, rotation, zoom, mirror ..etc)

#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer                                  |     Description                                                                  |
|:--------------------------:|:------------------------------------------------------:|
| Input                                  | 32x32x1 Grayscale image                                          |
| Convolution_1 5x5       | 1x1 stride, VALID padding, outputs 28X28X6                |
| RELU                                  |                                                                                              |
|Dropout                             |Keep probability = 0.5                       |
| Max pooling                    | 2x2 stride,  outputs 14x14x6                                    |
| Convolution_2 5x5       | 1x1 stride, VALID padding, outputs 10x10x16   |
| RELU                                  |                                                                                              |
| Max pooling                    | 2x2 stride,  outputs 5x5x16                                       |
| Fully connected_0        | Output = 400.                                                                 |
|Dropout                             |Keep probability – 0.5                                                 |
| Fully connected_1        | Output = 120.                                                                 |
| RELU                                  |                                                                                              |
| Fully connected_2        | Output = 84.                                                                   |
| RELU                                  |                                                                                              |
| Fully connected_3        | Output = 43.                                                                   |
 
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used baseline LeNet model in classroom material. However since the accuracy was very low at 
the beginning I added dropout layer and optimized the hyperparameters. Adam Optimizer is used similar to classroom material. Here are the hyperparameter values that eventually I settled with:

* Learning Rate: 0.001
* Epochs: 70
* Batch Size: 128
* Dropout: 0.5 (%50) is used for two layers


#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of % 99
* validation set accuracy of % 93
* test set accuracy of % 92

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?
    * I started with LeNet network given in the classroom tutorial as a starting point.
    

* What were some problems with the initial architecture?
    * Initially accuracy as very low (underfiting). I added two dropout layers and tuned the hyperparameters. (Epochs, batch size, learning rate, keep prob)


* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
    * Dropout layers are added for avoiding overfitting. And also input layer had to be changed to 32x32x1 since we are using grayscale images.


* Which parameters were tuned? How were they adjusted and why?
  
  * Learning rate, # of epochs and batch size is tuned.
    * Learning Rate: Increasing learning rate makes the model training faster however decreasing it makes training process slower whereas it also provides the lowest possible loss.
    * Number of epochs: I increased the number of epochs to a limit where model starts to overfit. In my model I chose 70.
    * Batch Size: Since we have limited memory we can not train the all data set at once. So we split it into batches to train the model. In my application I choose 128.
    * Keep Probability: I added two dropout layers with %50 keep probability to prevent overfitting.


* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model? 
  
    * Dropout basically prevents model to train in a lazy way. It helps avoding model to learn repetitive -and basically useless- features so that model can work in real (test) world.

 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are eight German traffic signs that I found on the web:

![alt text][image5] ![alt text][image6] ![alt text][image7] 
![alt text][image8] ![alt text][image9] ![alt text][image10]
![alt text][image11] ![alt text][image12]


#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

![alt text][image13]



The model was able to correctly guess 7 of the 8 traffic signs, which gives an accuracy of 87.5%. This compares favorably to the accuracy on the test set of %92

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 17th code cell of the Ipython notebook.

```python
test_labels = [34,12,1,14,25,11,18,38] # Correct labels for test data -in order


with tf.Session() as sess:
    sess.run(tf.global_variables_initializer())
    saver3 = tf.train.import_meta_graph('./lenet_project.meta')
    saver3.restore(sess, "./lenet_project")
    my_accuracy = evaluate(test_images_normalized, test_labels)
    print("Test Set Accuracy = {:.3f}".format(my_accuracy))
```

For 7 of the images, the model is relatively sure for its prediction. However, for the 5th picture (Roadwork) model seem to be struggling and making false predictions.
From the softmax probabilities it can be seen that model confuses and predicts as "wild animals crossing" label.
This is because both signs have a similar shape (red triangle wih some black dots inside). Model can be tuned further to avoid this problem by simply increasing number of images for both class by applying augmentation methods given above.

![alt text][image14]




### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?



