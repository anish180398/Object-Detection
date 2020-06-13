
Object Detection using YOLO model

Real-time object detection and classification

Dependencies

1. Python3
2. tensorflow 1.0
3. numpy
4. opencv 3

Training new model

Training is simple as you only have to add option --train. Training set and annotation will be parsed if this is the first time a new configuration is trained. To point to training set and annotations, use option --dataset and --annotation. A few examples:

# Initialize yolo-new from yolo-tiny, then train the net on 100% GPU:
flow --model cfg/yolo-new.cfg --load bin/yolo-tiny.weights --train --gpu 1.0

# Completely initialize yolo-new and train it with ADAM optimizer
flow --model cfg/yolo-new.cfg --train --trainer adam
During training, the script will occasionally save intermediate results into Tensorflow checkpoints, stored in ckpt/. To resume to any checkpoint before performing training/testing, use --load [checkpoint_num] option, if checkpoint_num < 0, darkflow will load the most recent save by parsing ckpt/checkpoint.

# Resume the most recent checkpoint for training
flow --train --model cfg/yolo-new.cfg --load -1

# Test with checkpoint at step 1500
flow --model cfg/yolo-new.cfg --load 1500

# Fine tuning yolo-tiny from the original one
flow --train --model cfg/yolo-tiny.cfg --load bin/yolo-tiny.weights
Example of training on Pascal VOC 2007:

# Download the Pascal VOC dataset:
curl -O https://pjreddie.com/media/files/VOCtest_06-Nov-2007.tar
tar xf VOCtest_06-Nov-2007.tar

# An example of the Pascal VOC annotation format:
vim VOCdevkit/VOC2007/Annotations/000001.xml

# Train the net on the Pascal dataset:
flow --model cfg/yolo-new.cfg --train --dataset "~/VOCdevkit/VOC2007/JPEGImages" --annotation "~/VOCdevkit/VOC2007/Annotations"
