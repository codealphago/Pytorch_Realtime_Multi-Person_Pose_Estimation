## Pytorch Realtime Multi-Person Pose Estimation

This is a pytroch version of Realtime Multi-Person Pose Estimation, origin code is here https://github.com/ZheC/Realtime_Multi-Person_Pose_Estimation

## Introduction

Code for reproducing CVPR 2017 Oral paper using pytorch

## Results

<div align='center'>
<img src="https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/testing/ski.jpg", width="300", height="300">
&nbsp;
<img src="https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/testing/result.png", width="300", height="300">
</div>

## Contents
1.[preprocessing](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/preprocessing): some scripts for preprocessing data.

2.[training](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/training): some scripts for training networks.

3.[testing](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/testing): the test script and example.

4.[caffe2pytorch](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/caffe2pytorch): the script for converting.

5.[caffe_model](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/caffe_model): caffe model

## Require
[Pytorch](http://pytorch.org/): 0.2.0_3

[Caffe](http://caffe.berkeleyvision.org/): If you want to convert the caffemodel by your own.

## Instructions
[Mytransforms.py](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/Mytransforms.py): some transformer.

transformer the image, mask, keypoints and center points, together.

[CocoFolder.py](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/CocoFolder.py): to read data for network.

It will generate the PAFs vector and heatmap when get the image.

The PAFs vector's format as follow:

```
POSE_COCO_PAIRS = {
	{3,  4},
	{4,  5},
	{6,  7},
	{7,  8},
	{9,  10},
	{10, 11},
	{12, 13},
	{13, 14},
	{1,  2},
	{2,  9},
	{2,  12},
	{2,  3},
	{2,  6},
	{3,  17},
	{6,  18},
	{1,  16},
	{1,  15},
	{16, 17},
	{15, 18},
}
```
Where each index is the key value corresponding to each part in [POSE_COCO_BODY_PARTS](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/preprocessing/README.md)

[utils.py](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/BasicTool.py): some common functions, such as adjust learning rate, read configuration and etc.

[visualize_input.ipynb](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/visualize_input.ipynb): the script to vierfy the validaity of preprocessing and generating heatmap and vectors. It shows some examples.

[pose_estimation.py](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/training/pose_estimation.py): the structure of networks.

The first 10 layers equals to VGG-19, so if set pretrained as True, it will be initialized by the VGG-19. And the stage is 6. The first stage has 5 layers (3 3x3conv + 2 1x1conv) and the remainder stages have 7 layers (5 3x3conv + 2 1x1conv).

TODO: the stage is adjustable.

## Training steps

- Download the data set, annotations and [COCO official toolbox](https://github.com/cocodataset/cocoapi)
- Go to the "preprocessing" folder `cd preprocessing`.
- Generate json file and masks `python generate_json_mask,py`.
- Go to the "training" folder `cd ../training`.
- Set the train parameters in "config.yml".
- Set the train data dir , train mask dir, train json filepath and val data dir, val mask dir, val json filepath. 
- Train the model `sh train.sh`.


## Notice

- When you want to train some other datasets, please change the code: [Mytransforms.py](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/Mytransforms.py#L158), [CocoFolder.py](https://github.com/last-one/pytorch_realtime_multi-person_pose_estimation/blob/master/CocoFolder.py#125) to correspond to your datasets. Besides, please ensure '0' corresponds to background.
- The converted model and my code are used BGR to train and test images.

## Citation
Please cite the paper in your publocations if it helps your research:
	
	@InProceedings{cao2017realtime,
		title = {Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields}},
		author = {Zhe Cao and Tomas Simon and Shih-En Wei and Yaser Sheikh},
		booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
		year = {2017}
		}
