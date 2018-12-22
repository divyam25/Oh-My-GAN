

## Deep Convolutional Generative Adversarial Networks (DCGANs)
The idea behind GANs is to train two networks jointly:
1. A **generator** G to map a Z following a [simple] fixed distribution to the desired "real" distribution, and
2. a **discriminator** D to classify data points as "real" or "fake" (i.e. from G).

The approach is **adversarial** since the two networks have **antagonistic** objectives.

GANs have been known to be unstable to train, often resulting in generators that produce nonsensical outputs. There has been very limited published research in trying to understand and visualize what GANs learn, and the intermediate representations of multi-layer GANs. 

Following excerpt from the paper makes it quite evident : 

"**We also encountered difficulties attempting to scale GANs using CNN architectures commonly used in the supervised literature. However, after extensive model exploration we identified a family of architectures that resulted in stable training across a range of datasets and allowed for training higher resolution and deeper generative models.**"

Paper on DCGAN(Radford et.al 2015) proposes and evaluates a set of constraints on the architectural topology of Convolutional GANs that make them stable to train in most settings.

## Architectural settings Proposed
1. Replace any pooling layers with strided convolutions (discriminator) and **fractional-strided convolutions**  (generator) ; often miscoined as **Deconvolution**.
2. Use batchnorm in both the generator and the discriminator (stable gradient flow across layers)
3. Remove fully connected hidden layers for deeper architectures.
4. Use **ReLU** activation in generator for all layers except for the output, which uses Tanh. (bounded activation saturates the model quickly)
5. Use **LeakyReLU** (alpha = 0.2) activation in the discriminator for all layers (to avoid vanishing gradients)

## Training Details 
1. Images need to be rescaled to  **64 x 64**  before feeding to the network.
2. Adam optimizer was used with a mini batch size = 128
3. All weights were initialized from a zero-centered Normal distribution
with standard deviation 0.02. (still works fairly well without this tweak)
4. learning rate = **0.0002** overriding the default 0.001

![alt text](https://github.com/divyam25/Oh-My-GAN/raw/master/dcgan.png "Generator Configuration")

# Training Loss v/s Epochs : 
![alt text](https://github.com/divyam25/Oh-My-GAN/raw/master/content/MNIST_DCGAN_results/MNIST_DCGAN_train_hist.png "Loss Plot")

I will be running a few more epochs to check for any kind of improvements in Generator Performance further. 

## Results : 
1. With a uniform distribution **Z** constant for every epoch (same digit in the block throughout all epochs)
![alt text](https://github.com/divyam25/Oh-My-GAN/raw/master/content/MNIST_DCGAN_results/generation_animation_fixed.gif "fixed Z")
2. With a uniform distribution **Z** changing every epoch. (different digits in the block for different epochs)
![alt text](https://github.com/divyam25/Oh-My-GAN/raw/master/content/MNIST_DCGAN_results/generation_animation_random.gif "random Z") 

# References :
* "Unsupervised representation learning with deep convolutional generative adversarial networks." [[arxiv]](https://arxiv.org/pdf/1511.06434)
* https://pytorch.org/



