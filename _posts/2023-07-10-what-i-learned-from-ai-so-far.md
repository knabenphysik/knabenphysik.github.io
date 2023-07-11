---
layout: post
title:  "What i learned from ai so far?"
excerpt: "before touch neural net code, understand your data first is a good idea"
tags: ["deep learning"]
comments: true
---

This _hello world_ note spawn from [Jimmy's](https://htasia.com/jimmy-ng) internal training on _software development basic_.

Earlier, the _training_ of deep neural networks is very often limited by hardware (e.g. number of compute cores, memory, etc). Now, dedicated deep learning hardware is becoming common norm (GPU's) and even can be purchase easily.

However, past a certain point of model complexity (neural network algorithm), the limit arise again. Then we have to turn to the choosing of floating-point format , which can have a significant impact on your model training times and even [performance](https://docs.nvidia.com/deeplearning/performance/mixed-precision-training/index.html).


## Floating-Point in Deep Learning

For the purposes of deep learning we are only interested three: [FP16](https://en.wikipedia.org/wiki/Half-precision_floating-point_format), [FP32](https://en.wikipedia.org/wiki/Single-precision_floating-point_format) and [FP64](https://en.wikipedia.org/wiki/Double-precision_floating-point_format) (a.k.a. half-, single- and double-precision floating-point formats)[^1].

Let's take FP32 as an example. Each FP32 number is a sequence of 32 bits, $b_{31} b_{30} ... b_{0}$. Altogether, this sequence represents the real number

$$ (-1)^{b_{31}} \cdot 2^{(b_{30} b_{29} ... b_{23}) - 127} \cdot (1.b_{22} b_{21} ... b_{0})_2 $$

Here, $b_{31}$ (the _sign bit_) determines the sign of the represented value.

$b_{30}$ through $b_{23}$ determine the magnitude or scale of the represented value (notice that a change in any of these bits drastically changes the size of the represented value). These bits are called the _exponent_ or _scale bits_.

Finally, $b_{22}$ through $b_{0}$ determine the precise value of the represented value.  These bits are called the _mantissa_ or _precision bits_.

Obviously, the more bits you have, the more you can do. Here's how the three formats break down:

|      | Sign Bits   | Exponent (Scale) Bits | Mantissa (Precision) Bits |
| :--- | ----------: | --------------------: | ------------------------: |
| FP16 | 1           | 5                     | 10                        |
| FP32 | 1           | 8                     | 23                        |
| FP64 | 1           | 11                    | 53                        |

FP32 and FP64 are widely supported by both software (C/C++, PyTorch, TensorFlow) and hardware (x86 CPUs and most NVIDIA/AMD GPUs).

FP16, on the other hand, is not as widely supported in software. However, since deep learning is trending towards favoring FP16 over FP32, it has found support in the main deep learning frameworks (e.g. `tf.float16` and `torch.float16`). In terms of hardware, FP16 is not supported in x86 CPUs as a distinct type, but is well-supported on modern GPUs.

## Advice for Practitioners

We usually will consider lower floating point when, memory GPU is full or training time takes longer time!

[^1]: Technically, there are [quadruple-](https://en.wikipedia.org/wiki/Quadruple-precision_floating-point_format) and [octuple-precision](https://en.wikipedia.org/wiki/Octuple-precision_floating-point_format) floating-point formats, but those are pretty rarely used, and certainly unheard of in deep learning.

