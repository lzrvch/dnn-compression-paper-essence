## Hot papers on DNN compression (a-la awesome-dnn-compression)

* [Mixed precision] Mixed Precision DNNs: All you need is a good parametrization (ICLR 2020) [arxiv](https://arxiv.org/ftp/arxiv/papers/1905/1905.11452.pdf)

Consider symmetric uniform and power-of-two quantization, for each unifrom quantizer we learn not only the scale but also the bitwidth or the step size. Bitwidth and step size are rounded to nearest possible values on the forward pass, but their original value is being optimized during backprop. Authors show that parametrization in terms of scale and step size is the best (not with bitwdth), converges better (less noise) and lead to better generalization, because gradients w.r.t quantizer parameters are bounded. Authors propose a regularizer to limit the memory footprint of the network for both weights and activations. Learn <1% drop MobilenetV2 on Imagenet with the same size as a pure-int4 net. Cons: not optimized for inference, arbitrary bitwidths not suitable for CPU (10 bits, 6 bits etc.), weights and activations of the same layer do not have shared bitwidths.

* LSQ+: Improving low-bit quantization through learnable offsets and better initialization (Qualcomm 2020) [arxiv](https://arxiv.org/pdf/2004.09576.pdf)

Assymetric QAT with "smart" initialization. No evident novelty. Authors "introduce" asymmetric quantization for activations and unsigned symmetric for weights, which can be efficiently computed by pre-compiling zero-point to bias of convolution. 
Initialize weights by 3-sigma rule, find initialization for activation's quantizaters by minimization of quantization noise. 
Demonstrates better results than [PACT 2018](https://arxiv.org/pdf/1805.06085.pdf), [DSQ 2019](https://arxiv.org/pdf/1908.05033.pdf), [QIL 2018](https://arxiv.org/pdf/1808.05779.pdf).
Fully int4 EfficientNet-B0 has 2.3% of accuracy drop, fully int4 ResNet-18 - 0.7% of accuracy gain.

* HAWQ-V2: Hessian Aware trace-Weighted Quantization of Neural Networks (BAIR 2019) [arxiv](https://arxiv.org/abs/1911.03852)
* EBS: Efficient Bitwidth Search for Practical Mixed Precision Neural Network (2020) [arxiv](https://arxiv.org/pdf/2003.07577v1.pdf)
![GitHub Logo](/images/EBS_pipeline.png)
