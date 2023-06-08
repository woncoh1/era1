# ERA V1 S6 Part 2: Training a minimal CNN
> Train a minimal CNN using the MNIST dataset under constraints

## Problem
- Type: classification
- Task: handwritten digit recognition
- Data: MNIST dataset

## Goals
- Test accuracy > 99.4 %
- Number of parameters < 20,000
- Number of epochs < 20
- Use batch normalization and dropout
- Optionally use a fully connected layer or GAP (global average pooling)

## Methods
- Data augmentation (image transformation)
- Model architecture: fully convolutional neural network
- Loss function: cross entropy (= `nn.functional.log_softmax` + `nn.NLLLoss`)
- Weight optimizer: stochastic gradient descent with momentum (`optim.SGD`)
- Learning rate scheduler: `optim.lr_scheduler.StepLR`

## Results
- Test accuracy
    - Final: 99.57 % 
    - Maximum: 99.60 %
- Number of Parameters: 9,768
- Number of Epochs: 19
