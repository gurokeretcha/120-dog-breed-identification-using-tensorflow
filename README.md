# 120-dog-breed-identification-using-tensorflow
result: top 10% kaggle solution

## project Description:
This project is part of   [Kaggle's](https://www.kaggle.com/c/dog-breed-identification) Playground Prediction Competitions. The project is multi-class classification problem, where we need to classify dogs into one of the 120 breeds. Provided dataset is  [Stanford Dogs Dataset](http://vision.stanford.edu/aditya86/ImageNetDogs/) with 10222 training and 10357 test images.

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
- Set up mixed precision
- Data augmentation
- Model Callbacks
8. Training Models
- 8.1 Model_0: Baseline
- 8.2 Model_1: Improved Model
9. Evaluation Model Performance
10. Train on test set and make prediction
11. Custom Image Prediction (My GF's dog prediction)




### 1. Import Funtions and Libraries
- important libraries and provided
- Prepared [funtions](https://raw.githubusercontent.com/gurokeretcha/gurokeretcha/main/helper_funtions_ML.py) is download from my github repo

### 2. Understand the Data
- There are 10222 training and 10357 test images with 120 different classes.
- The breed distribution is shown bellow:
![alt text](https://github.com/gurokeretcha/120-dog-breed-identification-using-tensorflow/blob/main/output_imgs/download.png)


