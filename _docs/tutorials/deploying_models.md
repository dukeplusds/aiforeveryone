---
title: Deploying Models
category: Tutorials
order: 11
---

After we develop our models, we'll want to use them in real life situations. Many times, this will mean running data outside of our datasets on our models, and recording the results. Sometimes, however, we'll want to open our models up to the public, to other web services and software developers, or to other researchers. We can do this by developing an Application Programming Interface. This can be done using using many backend webframeworks, but here we're going to use [Flask](https://www.palletsprojects.com/p/flask/). Flask is a light-weight, minimal python based backend web framework.

Here, we'll import `json` and `io` from the standard python library. We'll also include `torch`, `torchvision` and `torchvision.transforms` from PyTorch. We'll import `PIL` for image processing. Lastly, we'll import `flask`, `jsonify` and `request` from `flask`.

```py
import io
import json

from torchvision import models
import torchvision.transforms as transforms
from PIL import Image
from flask import Flask, jsonify, request
```
We'll initialize our Flask application

```py
app = Flask(__name__)
```

We'll then include a json file for our dataset classes. We'll also use a pretrained model "densenet121" as our model to inference off of. If we've trained our own network, we could use that as a model, rather than a pretrained network. We'll set are model to `eval` for inferencing, much like we do in our "test" functions.

```py
imagenet_class_index = json.load(open('<PATH/TO/.json/FILE>/imagenet_class_index.json'))
model = models.densenet121(pretrained=True)
model.eval()
```

Next we'll define two functions, `transform_image` will 1) define our transforms, like we've done in previous scripts. We'll then open the incoming image using PIL's `Image.open` function. We'll transform the image and and return it.

```py
def transform_image(image_bytes):
    my_transforms = transforms.Compose([transforms.Resize(255),
                                        transforms.CenterCrop(224),
                                        transforms.ToTensor(),
                                        transforms.Normalize(
                                            [0.485, 0.456, 0.406],
                                            [0.229, 0.224, 0.225])])
    image = Image.open(io.BytesIO(image_bytes))
    return my_transforms(image).unsqueeze(0)
```

We'll also want to define a function to get our predictions... WIP

```py
def get_prediction(image_bytes):
    tensor = transform_image(image_bytes=image_bytes)
    outputs = model.forward(tensor)
    _, y_hat = outputs.max(1)
    predicted_idx = str(y_hat.item())
    return imagenet_class_index[predicted_idx]
```

Lastly, we'll define a route to post our images to. Here we'll post to '/predict' which will take an image read the file, get the predictions, and return a json response with the class name and class id.

```py
@app.route('/predict', methods=['POST'])
def predict():
    if request.method == 'POST':
        file = request.files['file']
        img_bytes = file.read()
        class_id, class_name = get_prediction(image_bytes=img_bytes)
        return jsonify({'class_id': class_id, 'class_name': class_name})


if __name__ == '__main__':
    app.run()
```

Great! so the entire code should look like this:

```py
import io
import json

from torchvision import models
import torchvision.transforms as transforms
from PIL import Image
from flask import Flask, jsonify, request


app = Flask(__name__)
imagenet_class_index = json.load(open('<PATH/TO/.json/FILE>/imagenet_class_index.json'))
model = models.densenet121(pretrained=True)
model.eval()


def transform_image(image_bytes):
    my_transforms = transforms.Compose([transforms.Resize(255),
                                        transforms.CenterCrop(224),
                                        transforms.ToTensor(),
                                        transforms.Normalize(
                                            [0.485, 0.456, 0.406],
                                            [0.229, 0.224, 0.225])])
    image = Image.open(io.BytesIO(image_bytes))
    return my_transforms(image).unsqueeze(0)


def get_prediction(image_bytes):
    tensor = transform_image(image_bytes=image_bytes)
    outputs = model.forward(tensor)
    _, y_hat = outputs.max(1)
    predicted_idx = str(y_hat.item())
    return imagenet_class_index[predicted_idx]


@app.route('/predict', methods=['POST'])
def predict():
    if request.method == 'POST':
        file = request.files['file']
        img_bytes = file.read()
        class_id, class_name = get_prediction(image_bytes=img_bytes)
        return jsonify({'class_id': class_id, 'class_name': class_name})


if __name__ == '__main__':
    app.run()
```

We can now run our application by running `python app.py`..... WIP WIP WIP


