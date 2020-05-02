## Hot papers on DNN compression (a-la awesome-dnn-compression)

* [Mixed precision] MIXED PRECISION DNNS: ALL YOU NEED IS A GOOD PARAMETRIZATION (ICLR 2020) [arxiv](https://arxiv.org/ftp/arxiv/papers/1905/1905.11452.pdf)

* LSQ+: Improving low-bit quantization through learnable offsets and better initialization (Qualcomm 2020) [arxiv](https://arxiv.org/pdf/2004.09576.pdf)

Assymetric QAT with "smart" initialization. No evident novelty. Authors "introduce" asymmetric quantization for activations and unsigned symmetric for weights, which can be efficiently computed by pre-compiling zero-point to bias of convolution. 
Initialize weights by 3-sigma rule, find initialization for activation's quantizaters by minimization of quantization noise. 
Demonstrates better results than [PACT 2018](https://arxiv.org/pdf/1805.06085.pdf), [DSQ 2019](https://arxiv.org/pdf/1908.05033.pdf), [QIL 2018](https://arxiv.org/pdf/1808.05779.pdf).
Fully int4 EfficientNet-B0 has 2.3% of accuracy drop, fully int4 ResNet-18 - 0.7% of accuracy gain.


