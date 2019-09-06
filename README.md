# StyleGAN-Resolution-Convertor
A Google Colab notebook to convert your low-resolution StyleGAN models into higher-resolution checkpoints so you can continue training!

---> Just checkout the notebook for all details: 

https://github.com/tr1pzz/StyleGAN-Resolution-Convertor/blob/master/StyleGAN_resolution_conversion.ipynb

## Once you set the image resolution in train.py, this choice is hard-baked into the computation graph...
Nvidia's StyleGAN models are pretty great, and training your own models is a lot of fun.
Unfortunately the way the training code is set up, you have to specify the final image resolution before you start training.
The ultimate img resolution then affects the computation graph of your model.

Even though StyleGAN uses progressive layer growing, if you trained a StyleGAN at eg 256 resolution, you can't simply load in this checkpoint and 
start finetuning it towards eg 1024 resolution because the variable names in the computation graph are different.

## Work-around by editing variable dicts
This simply script loads a small StyleGAN model and changes the variable dict so that the weights can be copied into a larger model for finetuning towards a higher resolution.

## There are two options:
  1. Set a target resolution (eg 1024) and initialize a target network from scratch using random initialization
  2. Load in a larger (pretrained) StyleGAN network (of eg resolution 1024) and keep the weights from the biggest layers, while copying everything else from the input network

## Finetuning / Transfer learning Generative models
Finetuning & transfer training GANs on similar / entirely different datasets is currently a bit of a dark art:
  - Should you copy the weights from the larger network? Or initialize those layers from scratch?
  - What about the discriminator: copy a pretrained one, or start from scratch?
  - What about learning rates, lod blending, data augmentation?
  
--> If you have experience with these things, feel free to pm me on Twitter: @xsteenbrugge
