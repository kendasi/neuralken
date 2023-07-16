# neuralken
A package to create feedforward neural networks in a short amount of code, mostly for beginners. Neuralken is under the MIT license.

## Documentation
Before starting, please note that there is a bug that hasn't been fixed yet that causes models with a single output to increase the error rather than decreasing during training. It still works fine for models with multiple outputs.
### Installing and importing neuralken
In this example, you'll be shown how to create a simple [XOR](https://en.wikipedia.org/wiki/XOR_gate) neural network. If both the inputs are the same, the model will output [0,1], but if they are different, they will output [1,0].
Before starting, pip install the latest version of the neuralken library. In your computer's terminal or shell, run:
```
pip install neuralken
```
Then, at the start of your code, import `neuralnetwork` from neuralken, like so:
```
from neuralken import neuralnetwork
```
### Training the model
To train a neural network, first you'll need to define a few variables:
```
trainingDataInputs = [[0,1], [1,0], [1,1], [0,0]]
trainingDataOutputs = [[1,0], [1,0], [0,1], [0,1]]
nodes = [10,10,10,10,10,10,2]
types = ["relu", "relu", "relu", "relu", "relu", "relu", "logistic"]
```
Let's break this down. On the first line, `trainingDataInputs` is defined, which is an array containing a few sub-arrays. Each sub-array is the inputs for one training example. 

On the second line, `trainingDataOutputs` is defined. It's another array containing a few sub-arrays. Each sub-array contains the desired outputs for the training example - where each element of the sub-array is for one output node. **Note that the input and output training data arrays should match up**. For example, the first sub-array of `trainingDataInputs` should match up with the first sub-array of `trainingDataOutputs`.

On the third line, the array `nodes` is defined. Each element of this array should be an integer. The number of elements in this array is the number of hidden layers, plus the output layer. Each number in this array is how many nodes are in the layer. This variable should only include the hidden and output layers, **not the input layer**.

Finally, on the fourth line, is the `types` array. Each element of this array defines the activation function of that layer, where each element is one layer of the network. This array should match up with the `nodes` array. The activation functions can include:
+ logistic
+ binary
+ linear
+ relu
+ tanh

Note that having multiple layers in a row that use tanh or linear activation functions may cause an error, because it could cause the outputs to get too large for python to handle.

Next, after defining the needed variables, we can train the network. Here's the code example:
```
optimalWeights = neuralnetwork.trainModel(trainingDataInputs, trainingDataOutputs, nodes, 350, 0.1, types)
```
In this code, `optimalWeights` is the set of weights that the model wants to work out, which gets learned during training. The trainModel function from the neuralken library is then used to work it out through back propagation. The `trainingDataInputs` and `trainingDataOutputs` arrays get fed in as arguments first, then the `nodes` array. The last argument is the `types` array. These were defined earlier. However, you'll notice that between `nodes` and `types` are two numbers: 350 and 0.1. 
+ 350 is the number of epochs used during training. This is how many times the model will run through the training data, adjusting it's weights. This number can be adjusted. Generally, a higher number of epochs increases the quality of the results of the trained network, however note that having it too high can cause your model to [overfit](https://en.wikipedia.org/wiki/Overfitting).
+ 0.1 is the learning rate. You can also adjust this value. This affects by how much the model adjusts it's weights each epoch. Setting it higher may make training faster and require less epochs, but having it too high may also cause the model to overfit.
### Running the model
To test the model, you'll need some of the variables defined in the last part, "Training the model". You should read that before this part.

You'll need to define some inputs for the network. We'll define them in a variable as an array:
```
inputs = [0,1]
```
Next, we'll run the `runNetwork` function, and store it in the variable `modelOutput`:
```
modelOutput = neuralnetwork.runNetwork(inputs, optimalWeights, nodes, types)[1]
```
The `optimalWeights` array was worked out during training in the previous section. `nodes` and `types` are hyperparameters, which were defined in the last section. At the end, [1] is needed to get the actual outputs of the model (index [0] is the outputs of the hidden layers only). You can then do whatever you need with the contents of modelOutput, such as return it to the user.
