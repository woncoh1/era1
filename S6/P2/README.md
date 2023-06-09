# ERA V1 S6 Part 2: Training a minimal CNN
> Train a minimal CNN using the MNIST dataset under constraints

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/woncoh1/era1/blob/main/S6/P2/A6.ipynb)

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

## Hyperparameters
- CenterCrop
    - size = 22
    - p = 0.1
- RandomRotation: degrees = (-15.0, 15.0)
- DataLoader: batch_size = 128
- Dropout2d: p = 0
- SGD
    - lr = 0.25
    - momentum = 0.9
- lr_scheduler.StepLR
    - step_size = 10
    - gamma = 0.1
- Number of training epochs = 19

## Receptive field
- r: receptive field size
- n: channel size
- j: jump
- k: kernel size
- s: stride
- p: padding
- conv: convolution layer
- tran: transition layer

| layer | r_in | n_in | j_in | k | s | p | r_out | n_out | j_out |
|-------|------|------|------|---|---|---|-------|-------|-------|
| conv1 |    1 |   28 |    1 | 3 | 1 | 0 |     3 |    26 |     1 |
| conv2 |    3 |   26 |    1 | 3 | 1 | 0 |     5 |    24 |     1 |
| conv3 |    5 |   24 |    1 | 3 | 1 | 0 |     7 |    22 |     1 |
| tran1 |    7 |   22 |    1 | 2 | 2 | 0 |     8 |    11 |     2 |
| conv4 |    8 |   11 |    2 | 3 | 1 | 0 |    12 |     9 |     2 |
| conv5 |   12 |    9 |    2 | 3 | 1 | 0 |    16 |     7 |     2 |
| conv6 |   16 |    7 |    2 | 3 | 1 | 0 |    20 |     5 |     2 |
| tran2 |   20 |    5 |    2 | 5 | 1 | 0 |    28 |     1 |     2 |

## Model summary
```
----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1            [-1, 8, 26, 26]              72
              ReLU-2            [-1, 8, 26, 26]               0
       BatchNorm2d-3            [-1, 8, 26, 26]              16
         Dropout2d-4            [-1, 8, 26, 26]               0
            Conv2d-5           [-1, 16, 24, 24]           1,152
              ReLU-6           [-1, 16, 24, 24]               0
       BatchNorm2d-7           [-1, 16, 24, 24]              32
         Dropout2d-8           [-1, 16, 24, 24]               0
            Conv2d-9           [-1, 16, 22, 22]           2,304
             ReLU-10           [-1, 16, 22, 22]               0
      BatchNorm2d-11           [-1, 16, 22, 22]              32
        Dropout2d-12           [-1, 16, 22, 22]               0
        MaxPool2d-13           [-1, 16, 11, 11]               0
           Conv2d-14            [-1, 8, 11, 11]             128
             ReLU-15            [-1, 8, 11, 11]               0
      BatchNorm2d-16            [-1, 8, 11, 11]              16
        Dropout2d-17            [-1, 8, 11, 11]               0
           Conv2d-18             [-1, 16, 9, 9]           1,152
             ReLU-19             [-1, 16, 9, 9]               0
      BatchNorm2d-20             [-1, 16, 9, 9]              32
        Dropout2d-21             [-1, 16, 9, 9]               0
           Conv2d-22             [-1, 16, 7, 7]           2,304
             ReLU-23             [-1, 16, 7, 7]               0
      BatchNorm2d-24             [-1, 16, 7, 7]              32
        Dropout2d-25             [-1, 16, 7, 7]               0
           Conv2d-26             [-1, 16, 5, 5]           2,304
             ReLU-27             [-1, 16, 5, 5]               0
      BatchNorm2d-28             [-1, 16, 5, 5]              32
        Dropout2d-29             [-1, 16, 5, 5]               0
           Conv2d-30             [-1, 10, 5, 5]             160
        AvgPool2d-31             [-1, 10, 1, 1]               0
          Flatten-32                   [-1, 10]               0
       LogSoftmax-33                   [-1, 10]               0
================================================================
Total params: 9,768
Trainable params: 9,768
Non-trainable params: 0
----------------------------------------------------------------
Input size (MB): 0.00
Forward/backward pass size (MB): 0.80
Params size (MB): 0.04
Estimated Total Size (MB): 0.85
----------------------------------------------------------------
```

# TODO
- [ ] Plot training and testing loss and accuracy curves
- [ ] Visualize example predictions
- [ ] Visualize sample training batch
