# cs639_vision_detection

## Problem
Our 

## Motivation Important?

## Current State Of Art

## Our Approach 
Our  instance centric attention network approaches to human-object interaction in three parts: detecting objects, construct prediction with human’s, object’s, spatial configuration perspective, and generating score confidence.
First, in order to detect human, R-CNN is used as selective search to localize people and object instances in the picture. Given the detected instances, our method aims to recognize interactions between all pairs of objects including human.
After searching our object detection, the model with CNN calculates the prediction of spatial relationship between human and objects for the next step called score fusion.

At the end of our approach,, computing the interaction confidence, we score the values by the above following equation. We compute the most closely related output with the score which depends on the confidence for the individual object detections. for each human-object interaction, we need to predict the Human object Interface score for each action A, where A denotes the total number of possible actions.
Through our approach, we can get the result with highlighting the detected human and object interaction in colored boxes.
On the left side,, our box shows our model can predict multiple situations in the given data, which means our model can detect different actions and objects in one human object.
On the right side, our model can predict more than one human box.
It represents our model can detect two or more interaction with their objects respectively.
This allow us to gather relevant contextual information facilitating Human Object Interaction.
With our project, the unexpected situations can be alerted and prevented.
Eventually, we can get the support in human’s activity cared by the supportive devices. 

For the terminology,
S a h o is the score for each action from the number of possible actions
S h or S o is the confidence for the individual object detections
s a h + s a o is the interaction prediction based on the appearance of the person sah and the object sao
sasp is  the score prediction based on the spatial relationship between the person and the object.
With calculation, the module detects the correlative scores in the human objective’s perspective.

## Results and comparison

## Discussion 
-what did you learn from this project?
-where could this lead to in the future? 




## Reference

