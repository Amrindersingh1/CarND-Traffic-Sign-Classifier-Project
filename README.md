# ** Amrinder's Traffic Sign Recognition** 

## Writeup

---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report

---
### Writeup / README

#### 1. Writeup / README that includes all the rubric points and how I addressed each one.

You're reading it! and here is a link to my [project code](https://github.com/Amrindersingh1/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Basic summary of the data set.

I used the numpy library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 4410
* The size of test set is 12630
* The shape of a traffic sign image is (32,32,3)
* The number of unique classes/labels in the data set is 43

#### 2. exploratory visualization of the dataset.

Here is an exploratory visualization of the data set:
![alt text](writeup/trainsetimages.PNG)

Here is the bar chart showing training set count for each label:
![alt text](writeup/trainsetlabelbarchart.PNG)



### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

For the preprocessing of images i decided to follow the what was taught in class and also on reading technical paper the technique were also used there to get good accuracy.
The first technique used was to convert all the images to grayscale.
Here is an example of a traffic sign image before and after grayscaling:
![alt text](writeup/gray.PNG)]

As a next step, I normalized the image data because on finding the mean of all three sets it was quite high so i decided to bring it close to zero which turnaround to be around 0.35
Here is an example of a traffic sign image before and after normalising:
![alt text](writeup/normalised.PNG)

As i visualized the count for each label of training set i found that there were a lot of classes with very less examples. It might create a problem for training model. so i decided to generate random images for all the labels to get count of each label around 4000.
The techniques I used were referred from the project 3 session held on zoom that applies random rotation and offset and position to images to generate more images.

The difference between the original data set and the augmented data set is the following:
![alt text](writeup/compare.png)



#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 GRAY image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| Max pooling	      	| 28x28x6 in, 14x14x6 out 				|
| ELU					|				activation								|
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 10x10x16 	|
| Max pooling	      	| 10x10x16 in, 5x5x16 out 				|
| ELU					|			activation |
| Flatten | input: 5x5x16 output: 400 |
| Fully Connected layer | input: 400 output: 120 |
| ELU | activation |
| Dropout | keep prob: 0.5 |
| Fully Connected layer | input: 120 output: 84 |
| ELU | activation |
| Dropout | keep prob: 0.5 |
| Fully Connected layer | input: 84 output: 43 |



#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an LeNet for starting and was able to get accuracy of around 93% for validation set on tuning the parameters.  For further improvement i added dropout layers to my model with keep probability of 0.5 and also used ELU as a activation function since it was giving me a better performance than RELU. The hyperparameters i used were after a lot trial and error and noting my results based on change in parameters.
Also I used the Adam optimizer. The final settings used were:
* batch size: 125
* epochs: 100
* learning rate: 0.0009
* mu: 0
* sigma: 0.1
* dropout keep probability: 0.5

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

As already discussed i started with basic LeNet architecture played aroung with parameters and when couldnt get model to get desired accuracy than worked on adding changes to model . Dropout was added alomg with ELU as activation function and a flattening layer . After changes to model i was able to achieve accuracy of around 95% so i decided to work with hyperparameters and after playing around with values and seeing what affets accuracy i came up with final set of hyperparameters to get desired accuracy.

My final model results were:
* validation set accuracy of 0.983
* test set accuracy of 0.96

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are German traffic signs that I found on the web:

![alt text](writeup/newimages.PNG)

My images seemed to more brighter than the training set with a lot of bright colors that might occupy different range in color space, possibly one model was not trained for.

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

The model was able to correctly guess all the traffic signs, which gives an accuracy of 100%. This was alot better than test set accuracy. I have added detailed image on new image predicition in next question.

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The top five soft max probabilities were

![alt text](writeup/softmax.PNG)

### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


