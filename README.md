#Homework 3

You must do the project individually. In this HW you will design a backdoor detector for 
BadNets trained on the YouTube Face dataset using the pruning defense discussed in 
class. Your detector will take as input:

1. B, a backdoored neural network classifier with N classes.
2. Dvalid, a validation dataset of clean, labelled images.
1. Output the correct class if the test input is clean. The correct class will be in [1,N].
2. Output class N+1 if the input is backdoored.

You will design G using the pruning defense that we discussed in class. That is, you will prune 
the last pooling layer of BadNet B (the layer just before the FC layers) by removing one 
channel at a time from that layer. Channels should be removed in decreasing order of average 
activation values over the entire validation set. Every time you prune a channel, you will 
measure the new validation accuracy of the new pruned badnet. You will stop pruning once the 
validation accuracy drops atleast X% below the original accuracy. This will be your new 
network B'.

Now, your goodnet G works as follows. For each test input, you will run it through both B and 
B'. If the classification outputs are the same, i.e., class i, you will output class i. If they differ you 
will output N+1. Evaluat this defense on:
  1. A BadNet, B1, (“sunglasses backdoor”) on YouTube Face for which we have already
told you what the backdoor looks like. That is, we give you the validation data, and
also test data with examples of clean and backdoored inputs.

Now you must submit:

  1. Your repaired networks for X={2%,4%,10%}. The repaired networks will be evaluated
using the evaluation script (eval.py) on this website https://github.com/csaw-hackml/
CSAW-HackML-2020. Everything you need for this project is under the "lab3" directory.
  2. Please create and submit a link to a GitHub repo. with any/all code you have produced in
this project along with a readme that tells us how to run your code.
  3. A short report (at most 2 pages) that includes a table with the accuracy on clean test data 
and the attack success rate (on backdoored test data) as a function of the fraction of 
channels pruned (X).

├── data 

    └── cl
        └── valid.h5 // this is clean validation data used to design the defense
        └── test.h5  // this is clean test data used to evaluate the BadNet
    └── bd
        └── bd_valid.h5 // this is sunglasses poisoned validation data
        └── bd_test.h5  // this is sunglasses poisoned test data
├── models

    └── bd_net.h5
    └── bd_weights.h5
## 1.Dependencies
  1.Python 3.6.9  
  2.Keras 2.3.1  
  3.Numpy 1.16.3  
  4.Matplotlib 2.2.2   
  5.H5py 2.9.0   
  6.TensorFlow-gpu 1.15.2   
  
## 2.Data   
 1.Download the validation and test datasets from https://drive.google.com/drive/folders/1U7izqIiyud6gCkDcu5G2JZY2ZWNR2O8x?usp=share_link and store them under data/ directory.     
 2.The dataset contains images from YouTube Aligned Face Dataset. We retrieve 1283 individuals and split into validation and test datasets.   
 
 ## 3.Evaluating the Backdoored Model
The DNN architecture used to train the face recognition model is the state-of-the-art DeepID network.     

To evaluate the backdoored model, execute eval.py by running:  
    python3 eval.py clean validation data directory poisoned validation data directory model directory.  
