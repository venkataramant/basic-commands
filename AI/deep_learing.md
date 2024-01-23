# Deep Learning
    DL is a Neural Networks with 3 or more layers
    DL mitates how brain process data and make decisions
    DL is a complex and iterative process.
    Start with a random initialization and work towards the right values by trail and error.

# Applications of DL
    NLP
    Speech Recoginization
    Image Recognization
    Self-Driving cars
    Customer Experience, Health Care and Robotics

# Linear Regression

    A linear model (Relationship between 2 or more variables)
    y=ax+b or y=a1x1+a2x2+...+a10x10+B 

    y=Depdenent Variable
    x=Indepdent Variable
    a=Slope
    b=Intercept

# Building a linear Regression Model
    Goal is to determine values for Slope and Intercept.
    Start with Known Independent(x) and Depedent (y) values.
    Model gets complex with more and more independent variables.

    5=3a+b, 11=5a+b
    b=5-3a  11=5a+5-3a
    b=5-3a  6=2a
    b=5-3a  a=3
    b=5-3*3 a=3
    b=-4    a=3

# Logistic Regression

    a binary model, output/depedent (Y) is either ZERO or ONE

    Y Dependent Variable (0/1)
    X Indepdent variable
    A Slope
    B Intercept
    F Activatin function [to convert continous variables to a boolean value]

# Perceptron
    An algorithm for supervised learning for binary classification
    It represents a single cell in neural network, built on logistic regression.

    Difference is slope is called Weight and intercept is called Bias.
    Weight and Bias are building blocks of this formula.

    y=f(w1x1+w2x2....+w10x10+b)

# Artificial Neural Network
    A network of perceptrons, Perceptrons are called 'Nodes' in Neural Networks.
    Nodes are organized in layers. (DL has 3 or more layers)
    Each Node has weights,Bias and Function (WBF)
    Each Node is connected to all nodes in the next Layer*
    
    Input Layer(Initial Indepdent Variables) >> Hidden Layers(3 or more layers) >> Output Layers

# Training a ANN
    A model is represented by Parameters and HyperParameters

    Adjusting weights and biases until error is minized and accuracy is maximized.
    Improve model by adjusting layers, node counts and other hyper parameters.

    Use training data [ Known values of input(Indepdent Variables) and Output(Dependent variables)]
# Input Layer
    Vector is a tuple of one or more values.
    
    NumPy - Represents the feature variables for prediction
    Features* are like attribute or columns in a row [ Same as Indepedent variables?]
    Vector is like a row [A list of values]
    Sample is a real life representation/values in a row

    *** Input PreProcessing ***
        all Features need to be represented as Numeric value

        Input_Type      ==>  PreProcessing
    ---------------------------------------
    1. Numbers             Centering and Scaling
    2. Categorical         Integer encoding, one-host encoding
    3. Text                TF-IDF, Embeddings [Text Frequency Inverse Document Frequency]
    4. Image               Pixels  - RGB Representation
    5. Speach              Time series of numbers

    *** Stages ****
    RawData ===> Centering and Scaling ==> Transposed

# Hidden Layer
    1 or more layers
    Each Node learns something about the feature-target variables/relationship.

# Weights and Biases
    These are trainable parameters in an ANN.

    W*X+B=Y

    Representaions in Matrics
    W is m*n Matric
    X is n*1 Matric
    B is 1*m Matric
    Y is n*1 Matric

    [ w1, w2, w3, w4
      w5, w6, w7, w8] * [x1
                         x2
                         x3
                         x4]   +[B1,B2,B3,B4] =[Y1,Y2,Y3,Y4]
    

# Activation Functions
    Determine which nodes propagate information to the next layer.
    Filters and Normalizes
    Convert output to non-linear
    Critial in learing patterns

    Examples:
    ----------------
    Sigmoid     0/1
    TanH        -1 to 1
    ReLU        (0 if value<0; value otherwise) [Rectified Linear Unit]
    SoftMax     Vector of proabilities, with sum=1

# Output Layer
    Softmax activation is used for classification problems in final Layer.

# Back Propagate
    To adjust weights and biases to minimize the error [For each Node]

    Each Node in ANN contributes to overall error in predictions
    A Node's contribution is based upon its weights and bias

    Based upon delta(Difference between output and actual y value), to adjust weights and biases in the layer.
#    Gradient Descent Process
    Repeating the learning excercise
        Forward Propagation
        Estimate Error
        Backward Propagate
        Adjust Weights and Biases
# Batches and Epoch

    Batch: a set of samples sent through ANN in a one pass
    Training Data set is divided into 1 or more batches
    Cost is estimated and parameters are updated one batch at a time.
        2 Types
            a. Batch Gradient Descent [Entire traning set is tried in 1 batch]
            b. Mini-Batch Gradient Descent(size is power of 2) [Multiple batches - batch_size<trainig_set size]
    Epoch:
        No of times the entire training set is used to train an ANN model

# Validation and Testing
    "training data set"  80% of Sample
    "validation data set" 10% of Sample
    "test data set" 10% of Sample
    Validation:
        After each epoch and corresponding parameter updates, the model can be used to predict for the "validation data set"

        Based upon accuracy/loss, model can be fine-tuned and learning process continues.
    Test/Evaluation:
    After final learning, model will be tested/evaluation for performance and accuracy

# ANN Model
    Parameters
        Weights
        Biases
    HyperParameters
        Number of Layers, Nodes in each layer, activation function
        Cost functions, learning rate, optimizers
        Batch Size, epoch

    Predicition Process
        Same as Forward Propagation
        PreProcess and prepare inputs
        Pass Inputs to the first Layer
            Compute Y using weights,biases and activation function (WBaF)
            pass to the next layer
        Repeat process until output layer
        PostProcess output
# FQA
    PreProcessing Steps for Numeric Data
        Centering and Scaling
        One-host Encoding
        outlier removal
    Preferred Cost function for N-Class Classificaiton is "Categorical cross-entropy"

    Cost Functions
        RMSE
        MSE
        Binary Cross-Entropy
        Categorical Cross-Entropy.

# Example1
    IRIS Classification
    Input
        Sepal Lenghth/Width
        Petal Length/Width
    Target
        Setosa
        Versicolor
        Virginica
        



