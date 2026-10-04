---
type: atomic
tags: [ai/vision, ai/ml, ai/robotics]
date: 2026-10-04
---

# YOLO Object Detection

## Idea
YOLO ("You Only Look Once") finds and labels every object in an image in a single pass of one network, which makes it fast enough for live video and robots.

## Definition
Earlier detectors proposed thousands of candidate regions and ran a classifier on each, which was slow. **YOLO** reframes detection as one regression problem. A [[Convolutional Neural Network]] divides the image into an S×S **grid**; each cell predicts a few **bounding boxes** (centre, width, height), a **confidence** that a box contains an object, and class probabilities. Multiplying gives a class-specific score per box, a low threshold drops weak boxes, and **non-maximum suppression** removes duplicates that overlap the same object. **YOLOv2** added **anchor boxes** (predicting offsets from typical box shapes learned by clustering the training set), batch normalisation and multi-scale training, improving accuracy and recall. Later versions added feature pyramids for small objects and anchor-free heads. The trade-off has always been speed for a little accuracy, especially on small or tightly clustered objects. In agriculture, for example, a camera on a field robot can run a YOLO model trained on labelled crop and weed images to decide where to spray or pull, frame by frame.

## Tools
- **Ultralytics** — the most widely used modern YOLO family and training library (v5, v8 and later).
- **Darknet** — the original C framework from the YOLO authors.

## Source
Joseph Redmon, Santosh Divvala, Ross Girshick and Ali Farhadi, "You Only Look Once: Unified, Real-Time Object Detection" (CVPR 2016); Redmon and Farhadi, "YOLO9000: Better, Faster, Stronger" (CVPR 2017) introduced YOLOv2.

---

## Compass

**Roots** — *where this comes from*
It is a [[Convolutional Neural Network]] trained by [[Supervised Learning]] on images labelled with boxes.

**Paths** — *where this leads*
Each detection's [[Confidence Score]] needs a threshold tuned for the job: a weed sprayer wants high recall, a safety stop wants few false alarms.

**Neighbors** — *what lives nearby*
It is often the perception step in the same robot loop as a [[Particle Filter]] and a [[PID Controller]], and the models are built and fine-tuned in [[PyTorch]].

**Clash** — *what pushes against this*
One-pass speed costs accuracy on small and overlapping objects, and a detector trained in one field, season or lighting can fail quietly in another unless it is re-evaluated on new data.
