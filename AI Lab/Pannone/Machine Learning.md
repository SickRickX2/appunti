The machine learns how to solve a specific problem alone.
It learns through tunable parameters, machine learning can be categorized in two main types:
- **supervised learning** -> there is someone "helping" the model during the training. Together with the dataset we also provide the solution to the problem. -> *Two main classes* **classification** (labels are *discrete categories*) and **regression** (labels are *continuous quantities* ex: tries to predict the temperature of a room, price of an house, so on..)
- **unsupervised learning** -> we are not helping the model during the learning phase, we only provide the data without a solution. 

>[!tip] Custering - How does it work?
>In unsupervised learning the machine separates one by one the objects in the data set in groups (classes)

>[!note] Inference
>Second phase of the model.
>We provide only the problem and we expect the correct solution as output.

>[!note] Semi-supervised 
>We give solutions only for a selected part of the dataset

### Neural Networks
They try to resume our brain in a very very high level way, but of course they have some limitations.
Artificial NN didnt born like Neural Networks.

>[!tip] Perceptron
>Works like a neuron but has a flexible threshold, we can put a mathematical function as threshold, not only a fixed value. It was actually sufficient to "solve" the neuron.

cs came up with the *multi-level perceptron* so an artificial brain -> **Artificial Neural Network**.

Some perceptron are stacked one on top of the others, and we introduce the concept of **layers**.

>[!note] Layer
>A layer is a single column of stacked perceptron.

The smallest NN is composed by 3 layers:
- *input layer* -> it takes the input
- *hidden layer* -> where the parameters are tuned 
- *output layer* -> provides the result/output

The only thing to change to get more precision is to add more hidden layers.

>[!note] Backpropagation
>It's used when we don t get the expected output -> error, and we compute the derivatives to tune the hidden perceptron

### Important terms for ML
- **Batch**: subset of elements from the dataset for training
- **Epoch**: number of (complete) iterations over the whole dataset
- **Parameters**: the data related to the model that is tuned during the training
- **Hyperparameters**:  the data related to the model that must be set by us -> other "knobs" to tune that the model is not able to tune by himself, ex: how big should be the batch, how many iterations we need to do? ... and so on. We *must* tune for the model.

### Convolutional Neural Network
In CNNs there are three type of layers
>[!note] Convoutional Layers
>Uses filters that perform convolution operations. The parameters that are tuned are the kernels (not the edges like ANN).

>[!note] Pooling Layers
>They allows to reduce the size of the data needed between the layers. In particular *max* and *average* pooling are special kinds of pooling.

>[!note] 
