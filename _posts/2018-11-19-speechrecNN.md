---
layout: post
title: Normalizing flows and Variational Autoencoders for speech recognition (speech-to-text)
subtitle: 
bigimg: /img/path.jpg
tags: [multivariate statistics, machine learning]
---
# Speech Recognition Project 
After the recent developments in tts systems *FlowWaveNet*[paper](https://arxiv.org/abs/1811.02155) and *WaveGlow* \[ [github](https://github.com/NVIDIA/waveglow) ,  [paper](https://arxiv.org/abs/1811.00002) \]
it has become apparent that end-to-end speech transcription is a matter of time. This is an attempt to make a small AE model with the normalizing flows for that task. An autoencoder for speech frames is to be constructed. The continuous dynamics of frames and transitions are expected to be captured by transitions in the latent space. By training a flow, the transition matrix based modeling of the HMMs can be replaced by an MCMC technique on continuous space but with proposal distributions that are trained by the neural network. The speaker normalization is a part of the parametrization of the autoencoder,
hopefully making it flexible enough for speech style transfer ;).

Random notes for speech recognition with NN:

## 18/11/2018 
### Reading the data, first signal analysis results
* Found TIMIT dataset on Academic torrents
* Played around with transformation from stft/mel/invmel/invstft
* audio reconstruction quite good with 80 mel banks (what Andrew Senior mentions that Google uses in [this youtube video](https://www.youtube.com/watch?v=HyUtT_z-cms) )
* fourier size for 16khz: 512 samples (32ms) 
* overlap of half-window seems reasonable. 
* Again from Senior, 26 frames are suggested. This may be a bit excessive, perhaps I should also capture the transitions as some sort of parametrized norm/flow 

Goal is to squish the high input dimensions fast, with huge matrices and a lot of dropout. 
At the moment I have complex mel inputs for the network. I'm thinking of treating them uniformly - it doesn't make sense to simply discard them. The network should find out what to do with them.

