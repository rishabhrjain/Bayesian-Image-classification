# Bayesian-Image-classification

## GOAL:
The goal of this project is to classify digits by finding statistical features like mean, variance and then using Bayesian posterior probabilities to arrive at a decision. It shows how simple statistical features extracted from an image using Bayesian decision theory can be used to classify an image into a digit! 

### Data: 
The data consists uses a subset of images (with modifications) from the MNIST dataset. The original MNIST dataset (http://yann.lecun.com/exdb/mnist/) contains 70,000 images of handwritten digits, divided into 60,000 training images and 10,000 testing images. We use only images for digit “3” and digit “7” in this project. The data is stored in “.mat” files. 

Following are the statistics for the data you are going to use:
Number of samples in the training set: "3": 5713; "7": 5835
Number of samples in the testing set : "3": 1428; "7": 1458

THe following steps are followed: 

###  1. Data Transformation
    Each image is a 28X28 matrix containing hand written digits. We have to follow two steps to extract features of an image. 

Step 1: Feature extraction
Each image is stored as a 28x28 array of pixels. For each image i, compute two features: the mean mi and the standard deviation si of the 784 pixels
so each image i is now [mi, si] which are two features of the image

Step 2: Normalize the features

Using training dataset, for every feature calculated in previous step, we find M1, S1 which are mean and standard deviation for first feature. Similarly we calculate M2, S2. 

For every image i, 
Yi = [y1i, y2i] = [(mi – M1)/S1, (si – M2)/S2]

###  2. Density estimation

We assume that the 2-d feature space of X_normalize defined above, samples from each class follow a normal distribution. Using the maximum likelihood estimation method, we estimate the parameters for the 2-d normal distribution for each class/digit, using the respective training data for that class/digit.

A normal distribution is defined by 2 parameters - mean and variance. We need to calculate co-variance matrix if number of features >=2. 

### 3. Bayesian Decision Theory for optimal classification 
Now we know what are the distributions of features when image is digit 3 and digit 7. For any new image, we can calculate likelihood (using multivariate density equation) using parameters estimated on training data

### 4.  Training and testing error. 

Let's assume priors of both digits 3 and 7 are equal. 
since priors of both digits are equal, probability of digit given an image just depends on likelihood (using bayes theorem). 

We compare the results with the true label and add the probabilty of the incorrect correct class as the error. Its different when compared to accuracy. 

For example, if the true label is digit 3. Let's say model A predicts P(digit=3/X) = 0.8 and model B predicts P(digit=3/X) = 0.6. Here model B will be penalized more even though we will classify the digit as 3 i.e the model with less confidence will be penalized more. 

### 5. Accuracy
The accuracy of model is basically the percentage of digits that the model classified right. In this case since priors of digits 3 and 7 are equal i.e P(digit=3) = P(digit=7). 
so if likelihood(3) > likelihood(7), we classify as 3 else 7. 
