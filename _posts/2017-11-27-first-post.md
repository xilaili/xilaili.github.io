---
layout: post
title: "AOGNets: Deep AND-OR Grammar Network for Visual Recognition"
description: "AOGNets: Deep AND-OR Grammar Network for Visual Recognition"
comments: false
---

<center>Xilai Li, Tianfu Wu*, Xi Song and Hamid Krim (* corresponding author)</center>
<br>

**Abstract**: This paper presents a method of learning deep AND-OR Grammar (AOG) networks for visual recognition, which we term AOGNets. An AOGNet consists of a number of stages each of which is composed of a number of AOG building blocks. An AOG building block is designed based on a principled AND-OR grammar and represented by a hierarchical and compositional AND-OR graph. Each node applies some basic operation (e.g., Conv-BatchNormReLU) to its input. There are three types of nodes: an AND-node explores composition, whose input is computed by concatenating features of its child nodes; an OR-node represents alternative ways of composition in the spirit of exploitation, whose input is the element-wise sum of features of its child nodes; and a Terminal-node takes as input a channel-wise slice of the input feature map of the AOG building block. AOGNets aim to harness the best of two worlds (grammar models and deep neural networks) in representation learning with end-to-end training. In experiments, AOGNets are tested on three highly competitive image classification benchmarks: CIFAR-10, CIFAR-100 and ImageNet-1K. AOGNets obtain better performance than the widely used Residual Net and most of its variants, and are comparable to the DenseNet. AOGNets are also tested in object detection on the PASCAL VOC 2007 and 2012 using the vanilla Faster RCNN system andobtain better performance than the Residual Net.
<br><br>

[**Paper**](https://arxiv.org/abs/1711.05847)
<br>

## Motivation and Objective

The wisdom in designing better deep network architectures usually lies in finding a network topology which can support both exploring new features and exploiting existing features in previous layers. From the perspective of representation learning, skip-connections within a Residual Network (ResNet) contributes to effective features exploitation/reuse, and dense connection with feature maps being concatenated together in the densely connected network (DenseNet) leads to effective feature exploration, beside their contributions in resolving the gradient vanishing and/or exploding issues in optimization. The Dual Path Network (DPN) proposed a simple yet effective architecture which alternates skip connection and dense connection in forming network structure. **This paper presents a method of integrating compositional grammar and deep neural networks in a deeply collaborative manner in representation learning, which naturally embraces the wisdom, thus harnesses the best of both worlds in representation learning and potentially opens the door of introducing more levels of structures based on well-studied, sophisticated, yet intuitive grammar models and structured knowledge representation in deep representation learning. **
<br>

Grammar models are well known in both natural language processing and computer vision. Image grammar was one of the dominant methods in computer vision before the recent resurgence in popularity of deep neural networks. With the recent resurgence, one fundamental puzzle arises that grammar models with more explicitly compositional structures and more analytic and theoretical potential, often perform worse than their neural network counterparts. **The proposed method bridges the performance gap, which is motivated by and aims to show the advantage of two nice properties of grammar which are desirable in network engineering: (i) The flexibility and simplicity of constructing different types of structure topology based on a dictionary of primitives and a set of production rules in a principled way; and (ii) The highly expressive power and the parsimonious compactness of its explicitly hierarchical and compositional structure. Furthermore, the explainable rigor of grammar could be harnessed potentially to address the intepretability issue of deep neural networks.**
<br>

## Overview of the Proposed AOGNets
<img align="middle" src="{{ site.url }}/images/AOGNet-BuildingBlock.png" alt="..."> <br>
An AOGNet consists of a number of stages each of which is composed of a number of And-Or grammar (AOG) building blocks. Here, a 3-stage network is shown in (a) with 1 building block in the first and third stage and 2 in the second stage. (b) illustrates the AOG building block. The input feature map is treated as a sentence of N words (e.g., N=4). The And-Or graph of the building block is constructed to explore all possible parses of the sentence w.r.t. a binary composition rule. Each node applies some basic operation (e.g., an example is show in (d) adapted from the bottleneck operator in ResNets to its input. The inputs are computed as shown in (c). There are three types of nodes: an **And-node** explores composition, whose input is computed by concatenating features of its child nodes; an **Or-node** represents alternative ways of composition in the spirit of exploitation, whose input is the element-wise sum of features of its child nodes; and a **Terminal-node** takes as input a channel-wise slice of the input feature map (i.e., a k-gram). Note that the output feature map usually has smaller spatial dimensionality through the sub-sampling used in the Terminal-node operations and larger number of channels. We also notice that different stages can use different And-Or graphs (we show the same one in (a) for simplicity), and before entering the first AOG stage we can apply multiple steps of Conv-BatchNorm-ReLu or front-end stages from other networks such as ResNets (thus AOGNets can be integrated with many other networks).
<br>

## Results
<img align="middle" src="{{ site.url }}/images/AOGNet-results.png" alt="...">




