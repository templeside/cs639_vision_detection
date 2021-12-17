# cs639_vision_detection
###### Chaiyeen Oh, Chanwoong Jhon
[View Presentation](presentation.pptx)
---
## Introduction

Artificial Intelligence is a fast growing field that gives impact on everyday lives. For instance, it automatically filters spam, recommends Netflix movies to watch and detect cancer from medical documentations. Also supplementary AI, such as the Internet of Things and virtual reality, is changing how people work in every industry. So for AI, working with humans, maintaining economic values, adapting to new environments and learning to work is significant.
<br>

## Problem
<br>

In the perspective of machines, technologies should keep humans at the center of the systems. However, there are some limitations of machines visually recognizing descriptive phrases of human languages. For instance, if I were ordering a house robot to ‘grab a key on the table’, the robot would detect many keys correctly but don’t know which key I am specifically talking about.

<br> 

![](https://github.com/templeside/templeside.github.io/raw/main/problem.png)

<br>

Most of the Computer Vision studies focus on developed object detection algorithms of objects that mostly fill up the image, However, the relationship between two or more objects has more significant meaning of the overall image. For instance, even though all the images above have both a bicycle and a person, the interpretations for each image are different from each other due to its relationship between a person and a bicycle.
Rather than using object detection in a single label, our team wanted to try to detect relationships between objects and generate how humans would describe the same image in subject, predicate, object format such as “person riding horse”. 
<br>

## Motivation

<br>

![motivation_and_usage.png](https://github.com/templeside/templeside.github.io/raw/main/motivation_and_usage.png)

<br>



Identifying visual relationship is important because it’s hard to interpret context of the image due to the complex structure of human language. And this problem hinder development of the computer vision of multi-modal AI in which multiple data sources such as image, text and speech are all combined to act like what humans do inside their brain.

With visual relationship detection model, images will also be more accurately retrieved since it provides important cues of identification. And this technology can be later used for 
searching images in local computer, website, and GIf search bar 
detecting accidents in factory immediately. And generating description of videos that doesn’t have an audio for those who are blind

<br>

## Current State Of Art
Human Pose Estimation      |   Secondary Regions
:----------------------------:|:-------------------------:
![](human_pose_estimation.png)|  ![](Secondary_Regions.png)

Two examples that are used to predict visual relationship are human pose estimation and secondary region. When both approaches want to refer to an image as a person riding a horse, the estimation will first detect a person. And extract features around human pose key points but second approach will find overlapping region or union of the human and object. While both approaches use hand-designed attention map that’s centered on individual cues of object or human. We instead used end-to-end trainable attention-based methods called instance-centric-attention-network(ICAN) to detect more contextual information of the image.

<br>

## Dataset
In this project, we used V-COCO as a dataset for this project. Verbs in COCO (V-COCO) is a dataset that builds off COCO for human-object interaction detection. Because we need to detect object with predicate or action verb, it was a perfect match for training the model.

V-COCO is consist of:
- 10,346 images
- 16,199 person instances
- Each person 
  -  29 action categories
  -  no interaction labels including objects

<br>

## Our Approach
Our  instance centric attention network approaches to human-object interaction in three parts: 
   1. Object Detection
   2. Prediction: human centric, object, spatial configuration 
   3. Score Confidence.

<br>

### 1. Object Detection

<br>

In this project, we used Faster R-CNN to detect object detection. 

Faster R-CNN model is composed of two modules:
Deep fully convolutional network and Fast R-CNN detector 

Regional Proposal Network     |     Fast R-CNN detector 
:-----------------------------------:|:-------------------------:
![](r-cnn1.png)                      |  ![](r-cnn2.png)

The R-CNN is extracting the features based on a pre-trained convolutional neural network and classify the regional proposal to either the background or one of the object classes. With the R-CNN, we can detect the object fast. The RPN implements the terminology of neural network with attention to tell the object detection (Fast R-CNN) where to look.
The RPN module is responsible for generating region proposals to detect. It applies the concept of attention in neural networks, so it guides the Fast R-CNN detection module to where to look for objects in the image.
Fast R-CNN detector filters out the pre-computed image features to filter out the object candidates.
Both modules Regional Proposal Network and Fast R-CNN detector find the featured region first and drop the less probability scores on the region.
### 2. Prediction Models

![](algorithm.png)

Using instances from object detection, we generated the Human Object Interaction hypothesis to compute action prediction scores
For human/object stream to detect human/object cues, we extracted the instance-level appearance feature for a person/object and contextual features based on the attentional map. And then we concatenated and pass it through two connected layers to produce the action scores
For pairwise stream, we took the union of two boxes and construct a binary image with two channels. And then, we extracted spatial features from this two-channel binary image by using CNN. Finally, to differentiate similar action prediction such as riding and walking a bicycle, we concatenated the spatial feature with human appearance feature. 

### 3. Score Confidence

The Score Confidence is the calculation based on the correlation with the streams:
1. Score based on human/object appearance and contextual features. (iCAN module)
2. Score based on the spatial relationship of human-object. (Spatial Configuration)
3. The final prediction is calculated by combining the interaction prediction calculated from each stream.

This inference can be implemented as an expression as follows:
![](equation.png)

On the expression:

![](saho.png) is the score for each action from the number of possible actions

![](sh.png) or ![](so.png) is the confidence for the individual object detections

![](sah+sao.png) is the interaction prediction based on the appearance of the person sah and the object sao
 
![](sasp.png) is  the score prediction based on the spatial relationship between the person and the object.
With calculation, the module detects the correlative scores in the human objective’s perspective.

<br>

## Result and Discussion
Multiple Interaction      |  Multiple human object
:---------------------------:|:-------------------------:
![](person.png)          |  ![](bicycle.png)

<br>

Through our approach, we were able to highlight human and object interaction in colored boxes as shown on the above. On the left detection, our box shows our model predict multiple interactions in a person
On the right detection, our model predict more than one human interaction.
This allow us to gather relevant contextual information facilitating Human Object Interaction. In future work, we can get the automated support by detected human’s activity cared by the vision powered devices. With our project, the unexpected situations can be alerted and prevented.


## References
<https://paperswithcode.com/dataset/v-coco>

<https://www.researchgate.net/figure/Pose-estimation-and-action-recognition-results-on-the-V-COCO-Dataset-16-which-has_fig9_339477856>

<https://arxiv.org/abs/1608.00187>

<https://arxiv.org/abs/1808.10437>

<https://blog.paperspace.com/faster-r-cnn-explained-object-detection/>

