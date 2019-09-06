# StyleGAN-Resolution-Convertor
A Google Colab notebook to convert your low-resolution StyleGAN models into higher-resolution checkpoints so you can continue training!

Nvidia's StyleGAN models are pretty great, and training your own models is a lot of fun.
Unfortunately the way the training code is set up, you have to specify the final image resolution before you start training.
The ultimate img resolution then affects the computation graph of your model.

Even though StyleGAN uses progressive layer growing, if you trained a StyleGAN at eg 256 resolution, you can't simply load in this checkpoint and 
start finetuning it towards eg 1024 resolution because the variable names in the computation graph are different.

This simply script loads a small StyleGAN model and changes to variable dict so that the weights can be copied into a larger model for finetuning 
towards a higher resolution.

There are two options:
  - Set a target resolution (eg 1024) and initialize a target network from scratch using random initialization
  - Load in a larger (pretrained) StyleGAN network (of eg resolution 1024) and keep the weights from the biggest layers, while copying everything else from the input network
