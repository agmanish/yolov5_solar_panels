# **Solution Summary**


---



I annotated the 200 images using RoboFlow and was able to find:
* 97 instances of By Pass Diodes(BP)
* 32 instances of Dark Hot Spots (DHS)
* 37 instances of Light Hot Spots (LHS)

The dataset can hence be considered imbalanced. Another factor to consider is that the light hot spots are very similar to normal panels and hence pose a challenge which reduces the precision of their classification.



---



### **Train/ Val Split**
The 200 images were split into a 80:20 train:val split, with the intuition that if the model is exposed to 80% of the data it can learn enough to perform well over 20% of unseen data, as is the case in most educational systems where students can practise on a large number of solved problems to tackle a small number of unsolved ones. The 80:20 split is just the general values that this split takes while training DL models.



---



### **Pre-Processing and Augmentation**
I pre-processed the images by resizing the model to 416px*416px which is the input accepted by the YOLOv5 model. I also tiled the images since we are dealing with small-scale objects to be detected, this effectively zooms the detector in on small objects, but allows us to keep the small input resolution we need in order to be able to run fast inference. If the model was to be deployed I would have to take care of tiling and restitching of the stest images ince we have utilized tiling during training.

To account for the low number omf available images available, I augmented the dataset by vertically flipping the images and varying the brightness in a range of + or - 25% to obtain a more robust model that will perform better during robustness.

This meant the training dataset fed to the model had 1800 images after tiling and augmentation, and 200 val images after tiling.


---


### **Model and Loss Function**

I decided on using the YOLOv5 Model due to its small size and high speed of classiifcation, that is trained with a Generalized Intersection over Union loss function, which initially increases the predicted bounding box's size and slowly moves towards the ground truth.This achieves better precision, since we are using bounding boxes of regular aspect ratios and in general have non-overlapping classes.


---


