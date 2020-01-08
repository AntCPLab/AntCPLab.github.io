---
layout: default
title: Introducing TF Encrypted
parent: Blogs
nav_order: 1
---

# Introducing TF-Encrypted

[TF-Encrypted/TFE](https://tf-encrypted.io/) developed by [Dropout Labs](https://dropoutlabs.com/) is an easy-to-use framework for Secure Multi-party Computation (MPC) machine learning in TensorFlow. We have developed several projects based on TFE (e.g. The solution winning the iDASH2019 competition), and are actively contributing to TFE.

# Do MPC machine learning in five minutes with TF-Encrypted

Here's a simple example showing how to do collaborative machine learning on a vertical splitted database using TF-Encrypted. 

Suppose there's a dataset containing 7000 samples with 32 features, 16 of which is held by Alice, and the other 16 (and the label) is held by Bob. Alice and Bob wants to train on the joint dataset, but they don't want to send their raw data to each other.

The example dataset could be found here: [aliceTrainFile.csv](https://raw.githubusercontent.com/Alibaba-Gemini-Lab/tf-encrypted/master/examples/logistic/aliceTrainFile.csv)  and [bobTrainFileWithLabel.csv](https://raw.githubusercontent.com/Alibaba-Gemini-Lab/tf-encrypted/master/examples/logistic/bobTrainFileWithLabel.csv).

## Step 1. Prepare three machines and set up environments

Make sure the three machines are able to access each other via IP:Port, check python3 and pip3 is correctly installed, then install TensorFlow and TF-Encrypted on the three machines.

```shell
# python3 --version
Python 3.6.9
# pip3 --version
pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)
#pip3 install tensorflow==1.13.2
#pip3 install tf-encrypted
```


## Step 2. Edit the following file config.json

```json
{
    "alice": "machine1:port1",
    "bob": "machine2:port2",
    "crypto-producer": "machine3:port3"
}
```

## Step 3. Write TFE training code
We provide an example for Logistic Regression :  [common.py](https://raw.githubusercontent.com/Alibaba-Gemini-Lab/tf-encrypted/master/examples/logistic/common.py) , [training_alice.py](https://raw.githubusercontent.com/Alibaba-Gemini-Lab/tf-encrypted/master/examples/logistic/training_alice.py) , [training_bob.py](https://raw.githubusercontent.com/Alibaba-Gemini-Lab/tf-encrypted/master/examples/logistic/training_bob.py)  and [training_server.py](https://raw.githubusercontent.com/Alibaba-Gemini-Lab/tf-encrypted/master/examples/logistic/training_server.py). 

## Step 4. Copy the files to the same directory

Copy config.json , common.py , training_alice.py , aliceTrainFile.csv to  machine1; 

Copy config.json ,  training_bob.py , bobTrainFileWithLabel.csv to machine2;

Copy config.json ,  training_server.py to machine3;

## Step 5. Run!

Run the following command on the three machines, and the final model will be printed on machine1. 
```shell
python3 training_bob.py
python3 training_server.py
python3 training_alice.py
```

# Extra notes

## About crypto-producer
Currently a third-party crypto-producer is needed for complex tasks such as generating beaver triples, which means TF-Encrypted is a three-party (with honest majority) computation framework. 

We are making progress on eliminating the crypto-producer for the pure two-party case.

## Production usage
TF Encrypted is an experimental software and must be hardened before production environments.  
