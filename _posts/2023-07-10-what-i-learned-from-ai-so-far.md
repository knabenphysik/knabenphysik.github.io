---
layout: post
title:  "What i learned from ai so far?"
excerpt: "before touch neural net code, understand your data first is a good idea"
tags: ["deep learning"]
comments: true
---

This _hello world_ note spawn from [Jimmy's](https://htasia.com/jimmy-ng) internal training on _software development basic_.

Before 2012, before [AlexNet](https://papers.nips.cc/paper_files/paper/2012/hash/c399862d3b9d6b76c8436e924a68c45b-Abstract.html), _training_ of neural networks is very often limited by hardware (e.g. number of compute cores, memory, etc). Now (in 2023), dedicated hardware is becoming common norm (GPU's) and even can be purchase easily.

However, past a certain point of model complexity (bigger parameter or bigger data), the limit arise again. Then we have to turn to the choosing of floating-point format , which can have a significant impact on your model training times and even [performance](https://docs.nvidia.com/deeplearning/performance/mixed-precision-training/index.html).

## Floating-Point

Floating Point Precision is a representation of a real numbers through binary format. To communicate numbers to our computers, values must be translated to binary 1s and 0s, in which the order and sequence of digits matter.

## Floating-Point in Deep Learning

The most common Floating Point Precision formats are Half Precision [FP16](https://en.wikipedia.org/wiki/Half-precision_floating-point_format), Single Precision [FP32](https://en.wikipedia.org/wiki/Single-precision_floating-point_format) and Double Precision [FP64](https://en.wikipedia.org/wiki/Double-precision_floating-point_format), each with their own advantages, disadvantages, and usefulness in specific applications.

Let's take FP32 as an example. It uses 32 bits to store a floating-point number, consisting of a sign bit, an 8-bit exponent, and a 23-bit significand (also known as the mantissa). Each FP32 number is a sequence of 32 bits, $b_{31} b_{30} ... b_{0}$. Altogether, this sequence represents the real number

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

FP16, on the other hand, is not as widely supported in software. However, since deep learning is trending towards favoring FP16 over FP32, it has found support in the main deep learning frameworks (e.g. `tf.float16` and `torch.float16`). In terms of hardware, FP16 is not supported in x86 CPUs as a distinct type (recent 3rd Gen Intel® Xeon® (Cooper Lake) support the bfloat16 format), but is well-supported on modern GPUs.

## Advice for Practitioners

Please consider lower floating point when, memory GPU is full or training time takes longer time!
