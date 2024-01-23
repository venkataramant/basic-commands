
https://colab.research.google.com

# What
    Machine Learning and Neural Networks
    Bilogical and ANN
    Single Layer Perceptron

    Learn Predict Improve

    AI
        Subject to making machines think and act like humans
    ML
        Focus on enabling computers to perform tasks without explicit programming
    DL
        A subset of ML, a learing based on artificial neural networks (ANN)

# Activation Fucntion
    In a Perceptron to introduce nonlinearity into the model. This allows the perceptron to learn more complex patterns [liner model limited possible, non-linear more options]
# SingleLaper Perceptron (SLPs)
    Only one Perceptron/One Layer/ One Activation Function
    Mostly requires labelled data to train
# MultiLayer Perceptrons (MLPs)
    Learns from both linear and non-linear functions
    Can be Used for Both Regression nad Classification use-cases

    Regression    Use-Case : Predict Home selling Price
    Classfication Use-Case : Classify Home has a garage or not.

    Not required to have a labelled-data

   Pattern Finding to represent the data.

    *** Characteritics ***

    Feed-Forward Network
        Input Layer --> Hiddlen Layer--> Output Layer
    Multiple Layers of Perceptrons
    Perceptrons are connected to Perceptrons in next layer (Output to input)
    No Loops and Fully connected.

# Transfer and Activation Functions

    Transformation/Transforer Function 
        is a function that takes sum of (products of (Weight * Inputs ) and Bias , outputs a value.
    Activation Function 
        Is a special function to introduce the non-linearity to ANN.
    Both are executed in single computation node/Perceptron

    Activation Functions
    ReLu    [>0] Only Positive only
    Sigmoid [0 to 1]
    TanH    [-1 to 1]

    Set of Features (Inputs)
    y-Hat (Predicted value)
    Batch Size: set of inputs
    Loss function [Measured on single data instance]
    Cost Function Model's error on a group of objects/datasets.

        Formula:: Root Mean of Squared Error (RMSE)
    
# Types
    Feed-Forward Neural Network

    CNN- Convolutional Neurl Networks 
        Image Recognization/ Image Classification/Object Detection/Image Analysis
        NLP
    RNN - Recurrent Neural networks
    Transformer Architecture

# CNN Architecture
        Input Layer
        Conolution Layer
        Pooling Layer
            Max Pooling
            Average Pooling
            Helps to reduce no of computes and easy to process
        Fully Connected  Layer
        Output Layer

    eg:
        InputImage --> Convolutin Filter( Features Detector ) --> Feature Map(Output)
    
# RNN
    UnStructured Data [ Sequential]
        Time-Series DAta
        Audio/Video Data
        Image Data
        Text (Language) Data
        Social Media

    Structured Data [Non Sequential]
        Numeric Data
        Categorical Data.
        
        




