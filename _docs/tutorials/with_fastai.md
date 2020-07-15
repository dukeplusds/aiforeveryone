---
title: Combining PyTorch and FastAI
category: Tutorials
order: 6
---
FastAI is a high level library that sits on top of PyTorch. It allows us to easily develop models and cuts out much of the tedious code that we have to write. FastAI is a stand alone library that can train networks, using best practices for default hyperparameters and network settings. However, the library does not allow for lower-level network programming. In this example, we'll use the FastAI library in combination with PyTorch, to allow for custom network development, reducing the train and test fuctions to a few lines of code. Thank you to Jeremy Howard and the FastAI team for providing the original code, which can be [found here](https://github.com/fastai/fastai2/blob/master/nbs/migrating.ipynb)


Here, we'll include both the FastAI and FastAI Vision library..

```python
from fastai import *
from fastai.vision import *
```

...along with our typical PyTorch libraries

```python
import torch
import torch.nn as nn
from torchvision import datasets, transforms
```

We'll define a network using the nn.Sequential module from PyTorch. This should look similar to the PyTorch code that we've seen in previous tutorials

```python

class Net(nn.Sequential):
    def __init__(self):
        super().__init__(
            nn.Conv2d(1, 32, 3, 1), 
            nn.ReLU(),
            nn.Conv2d(32, 64, 3, 1), 
            nn.MaxPool2d(2), 
            nn.Dropout2d(0.25),
            nn.Flatten(), 
            nn.Linear(9216, 128), 
            nn.ReLU(), 
            nn.Dropout2d(0.5),
            nn.Linear(128, 10), nn.LogSoftmax(dim=1) 
            )
```

We'll define our hyperparameters

```python
batch_size = 256
test_batch_size = 512
epochs = 1
lr = 1e-2
```

We'll define our data transforms as usual

```python
data_transforms = transforms.Compose([
        transforms.ToTensor(), 
        transforms.Normalize((0.1307,), (0.3081,))
])
```

And we'll load in the MNIST dataset.

```python
train_data = datasets.MNIST('../data', train=True, download=True, transform=data_transforms)
test_data = datasets.MNIST('../data', train=False, transform=data_transforms)
```

Here is where things will change slightly. Instead of using PyTorch functions to load the data, we'll use the `DataLoader` function from the FastAI library, this is necessary for function calls later in our code. You will get an error if trying to use the PyTorch data loaders.

```python

train_loader = DataLoader(dataset=train_data, batch_size=batch_size, shuffle=True)
test_loader = DataLoader(dataset=test_data, batch_size=test_batch_size, shuffle=True)
```

We'll call our network as usual.

```python
model = Net()
```

Here we'll use the `DataBunch` call, also from the FastAI library. This function takes care of the `device` function, and transforms the data to load into the `Learner` function. 

The `Learner` function takes care of the train and test loops for us. This cuts out a ton of repetitive code that we'd rather not write.

```python
data = DataBunch(train_loader, test_loader)
learn = Learner(data, Net(), loss_func=F.nll_loss, metrics=accuracy)
```

We can then call `fit` or `fit_one_cycle` on our learner that we've defined above. The `fit_one_cycle` call allows us to train a network using Leslie Smith's 1cycle policy.

```python
learn.fit_one_cycle(epochs, lr)
```


<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: left;">
      <th>epoch</th>
      <th>train_loss</th>
      <th>valid_loss</th>
      <th>accuracy</th>
      <th>time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>0.134131</td>
      <td>0.046530</td>
      <td>0.985600</td>
      <td>01:55</td>
    </tr>
  </tbody>
</table>

