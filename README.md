# Diversifying the data of an American Sign Language Detector

Last term, I worked on an ongoing research project at IBM Watson MIT lab with four other scholars from Breakthrough Tech AI. Our goal was to optimize an American Sign Language (ASL) detection algorithm translating image data to text. Designing such an algorithm successfully, will have a great impact on communication amongst people with hearing difficulties and the ones who are not conversant with ASL. But more importantly, a successful solution of such a model will help pave the way to a significant issue of Machine Learning algorithms. The problem of achieving high predictive performance after a model has been compressed to fit on a small memory card, like the one on our smartphones. A real-world application of an ASL detector would be developing a mobile application, which translates in “real-time” videos to text.
In this article, I would like to share this learning journey with you. 
#### Contents: 
1)	Project overview: our approach, model, dataset, and hypothesis 
2)	Personal contribution
A.	Change the background color of original dataset
B.	Formation of experiments to test our hypothesis
3)	Experiments’ Results
4)	Future Work & Learning Outcomes
#### Project overview: our approach, model, dataset, and hypothesis 
The ASL detection algorithm is a classification problem, which predicts if an image is depicting a letter in ASL alphabet. Initially, the model was trained and tested on a homogeneous dataset. This poses an issue called “overfitting”, which is when a model has only learned from a particular set of data and fails to fit new unseen data. To address this problem, we decided to increase the data diversity in the following ways; 
•	taking our own images, 
•	finding more open source ASL image datasets on Kaggle, 
•	changing the background color of the original dataset
The model we trained was a Neural Network from PyTorch’s nn.Module class with a linear layer, which applies a linear transformation to the incoming data of the form:  y=xA^T+b. 
The original dataset consisted of 80,000 images, which we split to 70% training, 20% validation, and 10% test set. We can observe the similarity of the normalized data below, same skin color, lighting and background.  
![image](https://user-images.githubusercontent.com/70606645/218503596-e3b4b7c1-9602-4cbd-97c8-9f171aaca3ae.png)
Figure 1: Original Dataset
Our hypothesis was that due to the dataset’s uniformity, which the model was trained and tested on, it would not generalize well to new and unseen data.
#### Personal contribution
##### A.  Change the background color of the original dataset
One of the approaches to increase the diversity of the data, was to change the background color of the original dataset. I achieved this by, firstly, transforming the images to grayscale, which was a necessary step to perform the Canny Edge Detection from OpenCV library. An “edge” is a discontinuity of brightness in an image, which allows us to find the boundaries of objects. This was an essential process in order to differentiate the foreground, hence the hand, from the background in an image. After that, I removed the noise of the images with Gaussian blur. Alongside the hand detection though, another prominent edge was identified, which existed in the background. This was not allowing to properly calculate the area of the hands, the contour. To resolve it I tried removing the straight lines at the top of each image with the Hough Lines Transform. This method accidently removed lines sections in the hands, which led me to dilate the lines to reconnect them once again. Lastly, I found the hand contours and changed the background.  

Figure 2: Edge Detection on the left and Calculation of the hand contour on the right 

The variability and noise of the images did not allow all hand gestures to be correctly captured by the Canny Edge Detector, which led to many failed attempts, like the left image below. For this reason, I was not able to create a complete dataset of all letters in the ASL alphabet. Consequently, we settled on enlarging the data diversity with the addition of new datasets from Kaggle and taking our own pictures.

Figure 3: Successful attempt to change the background color on the right and failed one on the left

##### B.  Formation of experiment to test our hypothesis 
To prove the aforementioned hypothesis, I designed three rounds of experiments. First, training and testing the model on the original data. Secondly, training the model on the original data, but testing it on a new dataset. Lastly, training and testing on a mixed dataset, which combined the original and the new datasets. To better understand the results of each experiment, we utilized multiple visualizations, such as bar graphs, and heat graphs.    

#### Experiments’ Results
We evaluated the model’s performance after 40 epochs with the accuracy metric, which is calculated by dividing the number of correct predictions by the total number of predictions. The accuracy metric’s accessibility was the reason for choosing it. In the first round of experiments, model trained and tested on the original dataset, the performance was 100%. However, the accuracy score on the second experiment, model trained on original and tested on new dataset, dropped to 2%. The difference in these two experiments signified that our hypothesis about the model overfitting the data was correct.  

Figure 4: Results of three experiments

On the third and last experiment, model trained and tested on mixed dataset, the accuracy increased back to 100%. This result indicates the success of increasing the dataset’s diversity, which resembles the real world a little bit more than before. 

#### Future Work & Learning Outcomes
There is still a lot of work to be done to create a diverse dataset. In the future, images with a wide spectrum of skin tones need to be added to remove racial biases. Furthermore, a more refined edge detection algorithm should be implemented instead of the Canny Edge Detector to successfully complete the changing of the original dataset’s background color. Also, more metrics need to evaluate the performance of the model (precision, recall, etc.), as the accuracy score does not depict the full picture of its performance. Another important research to be made is finding ways to feed the model phrases instead of single letters. This is because people do not use one letter at a time to form a word or a sentence in ASL, but rather expressive gestures. Lastly, deploying the model through a mobile application would be the final step to assess how it functions in the real world.   

Through this project I learned a lot of pivotal lessons. There will always be improvements to be made in any project, thus trusting the process and being patient with myself, as well as communicating effectively in a team are key. Despite of the complexity of working with image data, I learned crucial preprocessing techniques, which I will use in the future. The last lesson I got from this project was to be flexible with not arriving to the desirable outcome I was initially hoping for. Taking a shift might be necessary temporarily, as I had never tried changing the background color of an image. Therefore, this learning process was immense, and I would recommend others to try it for themselves. 









