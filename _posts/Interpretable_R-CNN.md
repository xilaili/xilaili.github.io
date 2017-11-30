---
layout: post
title: "Interpretable R-CNN"
description: "Interpretable R-CNN"
comments: false
---

<center>Tianfu Wu*, Xilai Li, Xi Song, Wei Sun, Liang Dong and Bo Li (* corresponding author)</center>
<br>

**Abstract**: This paper presents a method of learning qualitatively interpretable models in object detection using popular two-stage region-based ConvNet detection systems (i.e., R-CNN). R-CNN consists of a region proposal network and a RoI (Region-of-Interest) prediction network. By interpretable models, we focus on weaklysupervised extractive rationale generation, that is learning to unfold latent discriminative part configurations of object instances automatically and simultaneously in detection without using any supervision for part configurations. We utilize a top-down hierarchical and compositional grammar model embedded in a directed acyclic AND-OR Graph (AOG) to explore and unfold the space of latent part configurations of RoIs. We propose an AOGParsing operator to substitute the RoIPooling operator widely used in RCNN, so the proposed method is applicable to many stateof-the-art ConvNet based detection systems. The AOGParsing operator aims to harness both the explainable rigor of top-down hierarchical and compositional grammar models and the discriminative power of bottom-up deep neural networks through end-to-end training. In detection, a bounding box is interpreted by the best parse tree derived from the AOG on-the-fly, which is treated as the extractive rationale generated for interpreting detection. In learning, we propose a folding-unfolding method to train the AOG and ConvNet end-to-end. In experiments, we build on top of the R-FCN [9] and test the proposed method on the PASCAL VOC 2007 and 2012 datasets with performance comparable to state-of-the-art methods.
<br><br>

[**Paper**](https://arxiv.org/abs/1711.05226)
<br>

## Motivation and Objective
<img align="middle" src="{{ site.url }}/images/aog_examples.png" alt="..."> <br>
Prediction without interpretable justification will have limited applicability eventually based on the intuitive fact that people could get frustrated if someone close to her/him did something critical without convinced explanation, let alone machine systems. So, it becomes a crucial issue of addressing machine’s inability to explain its predicted decisions and actions (e.g., eXplainable AI or XAI proposed in the DARPA grant solicitation), that is to improve accuracy and transparency jointly: Not only is an interpretable model capable of computing correct predictions of a random example with very high probability, but also rationalizing its predictions, preferably in a way explainable to end users. Generally speaking, learning interpretable models is to let machines make sense to humans, which usually consists of many aspects. So there has not been a universally accepted definition of the notion of model interpretability. Especially, it remains a long-standing open problem to measure interpretability in a quantitative way. This paper focuses on learning qualitatively interpretable models in object detection. We aim to rationalize the popular two-stage region-based ConvNet detection system, i.e. R-CNN~\cite{FastRCNN,FasterRCNN,RFCN} qualitatively with simple extension and without hurting the detection performance. 
<br>

## Overview of the Proposed Method
<img align="middle" src="{{ site.url }}/images/model_overview.png" alt="..."> <br>
This paper presents a method of learning qualitatively interpretable models in object detection with end-to-end integration of a generic top-down hierarchical and compositional grammar model and bottom-up ConvNets as shown above. We adopt R-CNN in detection, which consists of (i) A region proposal component for objectness detection. Class-agnostic object bounding box proposals, i.e. RoIs (Region-of-Interest), are generated either by utilizing off-the-shelf objectness detectors such as the selective search or by learning an integrated region proposal network (RPN) end-to-end. (ii) A RoI prediction component. It is used to classify and regress bounding box proposals based on the RoIPooling operator. RoIPooling computes equally-sized feature maps to accommodate different shapes of the proposals. By interpretable models, we focus on weakly-supervised extractive rationale generation in the RoI prediction component, that is learning to unfold latent discriminative part configurations of RoIs automatically and simultaneously in detection without using any supervision for part configurations. To that end, we utilize a generic top-down hierarchical and compositional grammar model embedded in a directed acyclic AND-OR Graph (AOG) to explore and unfold the space of latent part configurations of RoIs. There are three types of nodes in an AOG: an AND-node represents binary decomposition of a large part into two smaller ones, an OR-node represents alternative ways of decomposition, and a Terminal-node represents a part instance. 
<br>

In learning, we propose a folding-unfolding method to train the AOG and ConvNet end-to-end. In the folding step, OR-nodes in the AOG are implemented by MEAN operators (i.e., each OR-node computes the average sum of children nodes). In the unfolding step, they are implemented by MAX operators (i.e., each OR-node selects the best child node). The folding step is to integrate out all latent part configurations. The unfolding step is to maximize out the latent part configurations, explicitly inferring the best parse tree for each RoI per category, then classifying a RoI based on the scores of the inferred parse trees. The folding step is to ensure fair comparison between children nodes of an OR-node in the unfolding step since it is not reasonable to make decision on selecting the best child with parameters in the AOG not trained sufficiently, especially at the beginning with randomly initialized parameters. The final parse tree is used as the extractive rationale for a detected object, which is contrastive (competed with all possible part configurations in the AOG) and selective (only used all the part configurations derived from the AOG).
<br>

## Results
Please see details in the paper.
<img align="middle" src="{{ site.url }}/images/AOG772-d-1-example1_small.png" alt="...">




