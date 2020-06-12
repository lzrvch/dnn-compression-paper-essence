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
Vastly impoved [DNAS](https://openreview.net/pdf?id=BJGVX3CqYm), but still produces fully mixed distribution of bitwidth. It can be computed by Binary Decomposition of matrix multiplications, but leads to binary matrix multiplications with ~4x more elements then in original weights. For ResNet18 they have 1% better accuracy than FP32 baseline with compression ratio close to full-INT4, but do not quantize the first and the last layers, hard to compare.

* Movement Pruning: Adaptive Sparsity by Fine-Tuning (HuggingFace 2020) [arxiv](https://arxiv.org/abs/2005.07683)

* Training with Quantization Noise for Extreme Model Compression by (Facebook 2020) [arxiv](https://arxiv.org/pdf/2004.07320.pdf) 
2 main independent insights: 
1. Introduced extreme compression scheme by using Product Quantization. The values are uniformly quantized as usual. The main idea is to cluster all quantized values and round them to K centroids. Centroids are updated by K-means in the end of epoch and tuned by averaging gradients of their assigned elements. No need to store all weights, instead codebook of quantized values with integer indexes is used, which leads to extreme compression ratio. 
2. Improved training for extreme compressions by quantizing a random subset of weights on each forward. It allows to update not quantized weights outside of quantization ranges. In contrast, gradient of quantized weights is zero outside of the range. 
Results:  
Efficient-Net-B3 is compressed ~14x times with 1.5% of accuracy drop, it's like quantization into ~2.3 bits in average. RoBERTa is compressed ~13x times with 1.2% of accuracy drop.  
Pros & Cons: 
This idea is beneficial for extreme compression >8x (< int4). But shows slightly similar results for int8. Requires efficient kernel for multiplication of values stored in codebook. Or can be computed by kernels for uniform quantization with additional unpacking values for activations.
