# ERA V1 S6 Part 1: Backpropagation with spreadsheet
> Implement backpropagation of errors on a small feed-forward network using Excel spreadsheet

Questions
- How does backpropagation work?
- What is the effect of learning rate on training loss?

Tasks
- Implement backpropagation in a spreadsheet (i.e. calculate ∂E/∂w for all weights)
- Plot loss vs epoch curves for various learning rates (η = 0.1, 0.2, 0.5, 0.8, 1.0, 2.0)

(Please click to zoom in for details)
![backpropagation](https://github.com/woncoh1/era1/assets/12987758/f4baeb34-3c49-429b-9016-3b7c9f27487c)

## 1. Parts List
The model consists of neurons, weights, activation function and loss function:

### 1-1 Network
- 3 fully connected layers: input, hidden, output
- 2 neurons per layer
- Activation function: [sigmoid function](https://en.wikipedia.org/wiki/Sigmoid_function)
- Loss function: $${1 \over 2}\sum_{k=1}^n (t_k - p_k)^2$$ where n = number of output neurons, t = target value, p = prediction value of an output neuron

### 1-2 Neuron
- i1, i2: input-layer neurons
- h1, h2: hidden-layer neurons (linear summation)
    - a_h1, a_h2: sigmoid function (non-linear activation) applied to h1 and h2 
- o1, o2: output-layer neurons (linear summation)
    - a_o1, a_o2: sigmoid function (non-linear activation) applied to o1 and o2

### 1-3 Weight
1. Layer 1 → 2
    - w1: i1 → h1
    - w2: i2 → h1
    - w3: i1 → h2
    - w4: i2 → h2
2. Layer 2 → 3
    - w5: a_h1 → o1
    - w6: a_h2 → o1
    - w7: a_h1 → o2
    - w8: a_h2 → o2

## 2. Major Steps 
The following steps repeat in a loop:

### 2-1 Forward Pass (loss calculation)
Alternate linear summation and non-linear activation to calculate the loss value:
1. Linear summation
    - h1 = w1 * i1 + w2 * i2
    - h2 = w3 * i1 + w4 * i2
2. Non-linear activation
    - a_h1 = σ(h1) = 1 / (1 + exp(-h1))
    - a_h2 = σ(h2) = 1 / (1 + exp(-h2))
3. Linear summation
    - o1 = w5 * a_h1 + w6 * a_h2
    - o2 = w7 * a_h1 + w8 * a_h2
4. Non-linear activation
    - a_o1 = σ(o1) = 1 / (1 + exp(-o1))
    - a_o2 = σ(o2) = 1 / (1 + exp(-o2))
5. Loss function
    - E1 = 1/2 * (t1 - a_o1)²
    - E2 = 1/2 * (t2 - a_o2)²
    - E_total = E1 + E2 = E

### 2-2 Backward Pass (gradient calculation)
Apply the chain rule following the network topology:

1. Weights **after** hidden layer
    - ∂E/∂w5
    - ∂E/∂w6
    - ∂E/∂w7
    - ∂E/∂w8
2. **Branching** of gradient flow after hidden layer
    - ∂E/∂a_h1 = ∂(E1 + E2)/∂a_h1 = ∂E1/∂a_h1 + ∂E2/∂a_h1
    - ∂E/∂a_h2 = ∂(E1 + E2)/∂a_h2 = ∂E1/∂a_h2 + ∂E2/∂a_h2
4. Weights **before** hidden layer
    - ∂E/∂w1
    - ∂E/∂w2
    - ∂E/∂w3
    - ∂E/∂w4

### 2-3 Parameter Optimization (weight update)
wn = wn - η * ∂E/∂wn for all n weights:
- w1 = w1 - η * ∂E/∂w1
- w2 = w2 - η * ∂E/∂w2
- w3 = w3 - η * ∂E/∂w3
- w4 = w4 - η * ∂E/∂w4
- w5 = w5 - η * ∂E/∂w5
- w6 = w6 - η * ∂E/∂w6
- w7 = w7 - η * ∂E/∂w7
- w8 = w8 - η * ∂E/∂w8

## 3. Abbreviations
- i: input layer
- h: hidden layer
- o: output layer
- t: target label
- E: error (loss)
- a: activation function
- w: weight (parameter)
- ∂: partial derivative
- η: learning rate
- σ: sigmoid function
