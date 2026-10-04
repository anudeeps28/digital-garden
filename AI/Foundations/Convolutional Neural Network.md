---
type: atomic
tags: [ai/ml, ai/vision, ai]
date: 2026-10-04
---

# Convolutional Neural Network

## Idea
A CNN looks at an image through small learned filters that slide across it, so the same edge or texture detector works anywhere in the picture. Stacking these layers builds up from edges to shapes to whole objects.

## Definition
A **convolutional layer** applies a set of small filters (kernels, often 3×3) across the input; each filter computes a weighted sum at every position and produces a **feature map** showing where its pattern appears. The weights are **learned** during training, and because the same filter is reused everywhere (**weight sharing**), a CNN needs far fewer parameters than a fully connected network on raw pixels and naturally handles objects that move around the frame. A nonlinearity (usually ReLU) follows each convolution. **Pooling** layers (max or average) downsample the maps, making the network cheaper and more tolerant of small shifts. Early layers learn edges and colour blobs, middle layers textures and parts, and deep layers object-level features; a final classifier head turns those into labels. Modern variants add batch normalisation and residual connections (ResNet, 2015) that let networks go hundreds of layers deep. CNNs are the backbone of image classification, detection and segmentation, and are usually started from weights pre-trained on ImageNet and fine-tuned.

## Source
Kunihiko Fukushima's neocognitron (1980) introduced the layered architecture; Yann LeCun and colleagues trained convolutional networks with backpropagation for handwritten digits (1989) and published LeNet-5 (1998). AlexNet (Krizhevsky, Sutskever and Hinton, 2012) won ImageNet by a wide margin and started the deep learning boom.

---

## Compass

**Roots** — *where this comes from*
CNNs are trained by [[Supervised Learning]] on labelled images, and they are a few lines to define in [[PyTorch]].

**Paths** — *where this leads*
[[YOLO Object Detection]] puts a CNN backbone in front of a grid of box predictions to find objects in one pass.

**Neighbors** — *what lives nearby*
Like [[Principal Component Analysis]] they compress raw input into useful features, and the final layers produce a [[Vector Embedding]] that can be compared or searched.

**Clash** — *what pushes against this*
Vision transformers now match or beat CNNs at large scale by learning global relationships that convolution's local window misses, though CNNs remain cheaper and stronger on small datasets and edge devices.
