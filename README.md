# 120-dog-breed-identification-using-tensorflow
result: top 10% kaggle solution

## project Description:
This project is part of   [Kaggle's](https://www.kaggle.com/c/dog-breed-identification) Playground Prediction Competitions. The project is multi-class classification problem, where we need to classify dogs into one of the 120 breeds. Provided dataset is  [Stanford Dogs Dataset](http://vision.stanford.edu/aditya86/ImageNetDogs/) with 10222 training and 10357 test images. The model uses pre-trained models from [keras applications](https://keras.io/api/applications/).

## Set up Environment:
The easiest way to run the project is [google colab](https://colab.research.google.com/notebooks/intro.ipynb?utm_source=scs-index#recent=true).


## Table of content:
1. Import Funtions and Libraries
2. Understand the Data
3. Create Stuctured Folders
4. Visualize Input Images
5. Visualize Image Sizes
6. Get the training and test data from directory
7. Set up Training
- Data augmentation
- Model Callbacks
8. Training Models
- 8.1 Model_0: Baseline
- 8.2 Model_1: Improved Model
9. Evaluation Model Performance
10. Train on test set and make prediction
11. Custom Image Prediction (My GF's dog prediction)
12. Future Work




### 1. Import Funtions and Libraries
- important libraries and provided
- Prepared [funtions](https://raw.githubusercontent.com/gurokeretcha/gurokeretcha/main/helper_funtions_ML.py) is download from my github repo

### 2. Understand the Data
- There are 10222 training and 10357 test images with 120 different classes.
- The breed distribution is shown bellow:
![alt text](https://github.com/gurokeretcha/120-dog-breed-identification-using-tensorflow/blob/main/output_imgs/download.png)

### 3. Create Stuctured Folders
since all the training images are in the same folder, I will create a folders of each class and copy the each training image to its appropriate classes.

### 4. Visualize Input Images
we can visualize random training images in order to have good understanding what data we are using.
![alt text](https://github.com/gurokeretcha/120-dog-breed-identification-using-tensorflow/blob/main/output_imgs/download2.png)

### 5. Visualize Image Sizes
In order to know what will be optimal image size for training we need to visualize original image shapes. In this case we will use (331,331) image shape for training because later in transfer learning `NASNetLarge` requires 331,331 size.
![alt text](https://github.com/gurokeretcha/120-dog-breed-identification-using-tensorflow/blob/main/output_imgs/download3.png)

### 6. Get the training and test data from directory
- imported traing and test images as 32 batches and (331,331) img size using `tf.keras.preprocessing.image_dataset_from_directory`. and also we create a tensor with all the images.

### 7. Set up Training
- we have created data augmentation layer(however we do not use this layer, because our model still have good performance, but it can also be tried later)
- created model callbacks such as checkpoint_callbacks, early_stopping, reduce_lr, learning_rate_scheculer, tensorboard_callback. some of the callbacks are not used in this project, but can be used later for further improvements.
### 8. Training Models
#### - 8.1 Model_0: Baseline
baseline model is created using transfer learning feature extraction(used EfficientNetB0). Input examples are split into 2 parts, training and validation images (70%/30%). early_stopping stopped training after 11 apochs and as the models shows the **accuracy score on validation images is 0.8438**. 
### - 8.2 Model_1: Concatination of different pre-trained models.
our goal is to imporve evaluation score and generalize the model performance as well. That is why we use The best pre-trained model feature extraction Concatination. 
we  use models such as : NASNetLarge, InceptionResNetV2, Xception and EfficientNetB7. our goal is to extract feature from each pre trained model and concatinate those features horizontally. As it shows in the end, after concatination we get feature map with the shape of 10222 x 10176. and after 12 epochs the **evaluation score on validation set is 0.9428** which is a huge improvement from previous models. Also if we look at the training history, even though the validation accuracy is not improving the same way as training accuracy, the overall model generalization still exist.
![alt text](https://github.com/gurokeretcha/120-dog-breed-identification-using-tensorflow/blob/main/output_imgs/download4.png)

### 9. Evaluation Model Performance
- as confusion matrix shows, the model finds it difficult to distinguish collie vs border_collie, siberian_husky vs eskimo dog, american_staffordshire_terrier vs soft_coated_wheaten_terrier
![Confusion Matrix](https://github.com/gurokeretcha/120-dog-breed-identification-using-tensorflow/blob/main/output_imgs/confusion_matrix.png)

- as F1 score plots last 11 classes have f1-score less than 85%. these can be improved by providing additional images of these classes and cleaning the data
![F1 Score of each classes](https://github.com/gurokeretcha/120-dog-breed-identification-using-tensorflow/blob/main/output_imgs/download6.png)

### 10. Train on test set and make prediction
- we create a concatinated feature map for test images and make prediction with the model_1. 
- uploaded Submision_test_dataset.csv to kaggle.
- Result on kaggle: 0.18239
![F1 Score of each classes](https://github.com/gurokeretcha/120-dog-breed-identification-using-tensorflow/blob/main/output_imgs/res.png)



### 11. Custom Image Prediction (My GF's dog prediction)
I uploaded my girlfriend's dog called Duche which is retriever. and let's see what our model predicts:
![F1 Score of each classes](https://github.com/gurokeretcha/120-dog-breed-identification-using-tensorflow/blob/main/output_imgs/duchee.png)



### 12. Future Work
in order to improve model's performance we additional methods such as:
- data augmentation 
- fine tuning
- different combination of pre-trained models
- manual data cleaning
