---
layout: page
title: About
description: Course policies and information.
---

# About
{:.no_toc}

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{% assign overview = site.slides | where: "title", "Overview" | first %}
{{ overview.content }}


## Aims

 - Knowledge how to apply AI to problems from the creative industry.

 - Familiarity with basic ML-based algorithms and data structures to process digital media.

 - Ability of dealing with large scale data and training of machine intelligence.

 - Knowing rephrasing of existing concepts from digital media with tools from AI.

 - Awareness of the difficulty of computed results and artistic freedom.

## Learning Outcomes

SKILL: Ability to formulate the diversity of image analysis and synthesis tasks as a machine learning process.

KNOWLEDGE: Theoretical and practical concepts allowing image processing and generation to become learnable and basic understanding of how to execute that learning.

ATTITUDE: Processing of visual data has to be optimized in respect to data.


## Topics

**Basic regression:** Ability to explain basic (1D) data with a linear model and to make predictions. Knowledge of how what a linear model entails, also in higher dimensions. The resulting attitude could be both that a surprisingly simple thing can explain complex visual phenomena, yet others it cannot.

**Understanding of linearity and non-linearity:** Participants will be able to judge if a linear or nonlinear model is adequate and how important non-linearity is for Visual Computing. They should have knowledge of how to represent such models. The key change in perspective is that almost all non-trivial processes are non-linear.

**Classification:** Ability to formalize a problem as classification code a simple classifier in. Knowledge that classification is regression over probabilities to be from a class.

**Neural networks:** Students should be able to code up a simple perceptron from scratch and manipulate its parameters (e.g., number of units and layers), as well as control the non-linearities. They would understand that NN is just matrix multiplications followed by non-linearities.

**Audio/2D/3D images and pixel processing:** Load and stored images/3D data, audio in the coding environment they use. Understand basic issues of sampling and representations like color and luminance. The attitude should be changing such that not only the algorithm matters, but also the right representation is critical.

**Tunable image filters:** convolutional neural networks: Participants will learn how to execute convolutions on images and how to set up their environment to optimize the parameters of the convolutions. The key knowledge is that learning convolutions allows to share learned parameters across the image.

**3D meshes and point clouds:** Until now data structures were regular, but now students will learn how to load irregular data (3D graphs, 3D meshes, 3D point clouds) into their environment and also how to process them as well as to learn tunable filters for them. They will deepen their knowledge of convolution by seeing how it extends to unstructured data, a generalization. The resulting attitude should be, that a well-defined convolution works on regular data as well as irregular ones.

**Ambiguity and style:** Students will be explained, that under some conditions, multiple solutions are valid and that it can be adequate to report any of these. They will see how to change their code from working on paired data matching an output to a reference, it can be sufficient to match only statistics. The required skill is to change the loss and choose the right representation of these statistics.

**Generative modelling:** We will first introduce the concept of a generative model, which takes simple parameters in low dimensions and maps them to complex objects in millions of dimensions. Using this requires the skill to load many exemplars and encode and decode them, which students can compose from components from before. The change of attitude should be, that a generative model is a very abstract way to “address” objects in a family of natural instances: images of faces, houses, cars, etc.

**Levels of supervision:** Adversarial training: Students here will acquire the skill to replace the supervision in form of pairs that are mapped to each other by a paradigm where only random samples form a target distribution are given. To this end they have to understand that the loss is replaced by another network.

