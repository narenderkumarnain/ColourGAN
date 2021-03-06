## ColourGAN
Simple PyTorch based GAN for colouring black and white images.

## Installation
The code is available as python package.
<br />
Run following command for installing colourgan with all it's dependencies.

```shell
pip install colourgan
```
Additionally for trying out streamlit interface, please install streamlit using following command
```shell
pip install streamlit
```
You can also install it from this repository.
```shell
git clone https://github.com/narenderkumarnain/ColourGAN.git
cd ColourGAN
python setup.py install
```

## Usage

### Inference
For trying our pretrained model, please download the 
[Generator Weight File](https://drive.google.com/file/d/1jPzTPKTrN8tWiLzRSh2hmY3PWxHC3LMF/view?usp=sharing)
<br />
Now use these lines of code for inference on sample image.
```python
#imports
import cv2
from colourgan.model import ColourGAN
from colourgan.config import get_cfg

# preparing the config
cfg = get_cfg()
# adding path to generator weights
cfg.initial_weights_generator = 'checkpoint_ep99_gen.pt'

# loading the model
model = ColourGAN(cfg , inference=True)

# loading the image
img = cv2.imread('sample.png')

# running inference
res = model.inference(img)

# saving result image
cv2.imwrite('sample_res.png' , res)
```

### Streamlit interface
For trying out the streamlit interface, create a file app.py with following code.
```python
# import
from colourgan.streamlit import app

# path to weights file
path_to_generator_weights = 'checkpoint_ep99_gen.pt'

if __name__ == '__main__':
    app(path_to_generator_weights)
```
We expect you have already installed streamlit.
<br/>
Use followind code to run the application
```shell
streamlit run app.py
```

## Training
Use following Lines of code for training the model on Cifar10 dataset.
```python
# imports
import torch
from colourgan.config import get_cfg
from colourgan.data import Cifar10Dataset
from colourgan.model import ColourGAN

# Downloading the data and creating the dataloaders
dataloaders = Cifar10Dataset('cifar10', batch_size = 8).get_dataloaders()

# config
cfg = get_cfg()

# creating the model
model = ColourGAN(cfg)

# train
model.train(dataloaders['train'],dataloaders['test'], epochs = 100)

```

## Pretrained Weights
[Generator](https://drive.google.com/file/d/1jPzTPKTrN8tWiLzRSh2hmY3PWxHC3LMF/view?usp=sharing)   
[Discriminator](https://drive.google.com/file/d/1IwdjRdYlUf2SwT4l0Fctfi51_dB7hNtP/view?usp=sharing)

## References
[GAN_image_colorizing](https://github.com/karoly-hars/GAN_image_colorizing)

[Colorizing-with-GANs](https://github.com/ImagingLab/Colorizing-with-GANs)


