## Traffic Sign Recognition

---

**Build a Traffic Sign Recognition Project**

Steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image4]: ./img1.jpg "Traffic Sign 1"
[image5]: ./img2.jpg "Traffic Sign 2"
[image6]: ./img3.jpg "Traffic Sign 3"
[image7]: ./img4.jpg "Traffic Sign 4"
[image8]: ./img5.jpg "Traffic Sign 5"


## Data Set Summary & Exploration

Here is a basic summary of the data used.

I used the Numpy library to calculate summary statistics of the traffic
signs data set:

* The size of training set is ? 34799 
* The size of the validation set is ? 4410 
* The size of test set is ? 12630 
* The shape of a traffic sign image is ? 32x32x3
* The number of unique classes/labels in the data set is ? 43

## Exploratory visualization of the dataset.


### 1.
As a first step, I Normalized all images in the training by subtracting each pixel from the mean of image and then deviding the result by the mean.

### 2.
I then augmented the data by filipping all images onece from left to right and another time from bottom to up. This tripled the size of my training set allowing me to train my network on larger number of examples.


The difference between the original data set and the augmented data set is the following: The size of training set is 104397 


## Network Model

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 7x7     	| 1x1 stride, valid padding, outputs 28x28x46 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x46 				|
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x56   |
| Max pooling           | 2x2 stride,  outputs 5x5x56                   |
| RELU	                |                                               |
| Fully connected		| 1400 input 300 output        				    |
| RELU                  |                                               |
| Fully connected      	| 300 input 54 output        				    |
| RELU					|												|
| Fully connected 		| 54 input 43 output 							|
 

I trained my model using AdamOptimizer with batch size of 128 and 30 Epochs and learning rate of 0.001


#### My final model results were:
* validation set accuracy of: 0.934 
* test set accuracy of: 0.917 


The first architecture used was Lenet, but since the training accuracy was not as high as expected I changed the architecture to exract more features in order to increase the accuracy to 0.92. Sice the accuracy on Validation set was also 0.91 this shows that over fitting did not occur. 


 ### Test a Model on New Images


Here are five German traffic signs that I found on the web:

![alt text][image4] ![alt text][image5] ![alt text][image6] 
![alt text][image7] ![alt text][image8]


Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Speed limit (30km/h)  |Speed limit (30km/h)  						    | 
| General caution    	| General caution 								|
|Right-of-way at the next intersection| Right-of-way at the next intersection|
| Pedestrians      		| No passing					 				|
| Slippery Road			| Right-of-way at the next intersection      	|


The model was able to correctly guess 3 of the 5 traffic signs, which gives an accuracy of 60%. The result of the new images is much lower than the result in test set. One reason that comes to mind is the fact that we resized these new images to 32x32 to be able to use the trained network. resizing the images have introduced distortion and as a result for example fo the sign of pedestrian in missclassifies it to no passing due to artifacts introduced by resizing the image. Same happens for other traffic signs. Finding images with smaller sized would have been better for this section, since resizing wouldn't be causisng it much artifacts.

