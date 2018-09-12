# Edit Moudle #
 Multi Scale Mudle에 맞게 설정이 되어있는 코드입니다.
 <p align="left">
<img src="https://github.com/ZheC/Multi-Person-Pose-Estimation/blob/master/readme/arch2.PNG", width="720">
</p>
 
 7X7 Convol 네트워크를 3X3 3개 + Concat + Eltwise-Sum 으로 변경되어 있습니다. -Please Check C3 (setLayers.py 193Line) 
 
 이에 맞춰 prototxt 파일도 Multi Scale Mudle에 맞추어 설정되어 있습니다.

 다르게 사용하기 위해선 setLayers.py코드에서 getBash() 부분을 수정해 주세요.

 또한 caffe_path, base_folder, dataFolder, source의 경로를 자신의 설정에 맞게 설정 해주세요.


# Realtime Multi-Person Pose Estimation
By [Zhe Cao](http://www.andrew.cmu.edu/user/zhecao), [Tomas Simon](http://www.cs.cmu.edu/~tsimon/), [Shih-En Wei](https://scholar.google.com/citations?user=sFQD3k4AAAAJ&hl=en), [Yaser Sheikh](http://www.cs.cmu.edu/~yaser/).

## Introduction
Code repo for winning 2016 MSCOCO Keypoints Challenge, 2016 ECCV Best Demo Award, and 2017 CVPR Oral paper.  

Watch our video result in [YouTube](https://www.youtube.com/watch?v=pW6nZXeWlGM&t=77s) or [our website](http://posefs1.perception.cs.cmu.edu/Users/ZheCao/humanpose.mp4). 

We present a bottom-up approach for multi-person pose estimation, without using any person detector. For more details, refer to our [CVPR'17 paper](https://arxiv.org/abs/1611.08050) or our [presentation slides](http://image-net.org/challenges/talks/2016/Multi-person%20pose%20estimation-CMU.pdf) at ILSVRC and COCO workshop 2016.

<p align="left">
<img src="https://github.com/ZheC/Multi-Person-Pose-Estimation/blob/master/readme/pose.gif", width="720">
</p>

This project is licensed under the terms of the [license](LICENSE).

Contact: [Zhe Cao](http://www.andrew.cmu.edu/user/zhecao)  Email: zhecao@cmu.edu

## Results

<p align="left">
<img src="https://github.com/ZheC/Multi-Person-Pose-Estimation/blob/master/readme/dance.gif", width="720">
</p>

<p align="left">
<img src="https://github.com/ZheC/Multi-Person-Pose-Estimation/blob/master/readme/shake.gif", width="720">
</p>

## Contents
1. [Testing](#testing)
2. [Training](#training)
3. [Citation](#citation)

## Testing

### C++ (realtime version, for demo purpose)
- Use our modified caffe: [caffe_rtpose](https://github.com/CMU-Perceptual-Computing-Lab/caffe_demo/). Follow the instruction on that repo. 
- In May 2017, we released an updated library [openPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose)
- Three input options: images, video, webcam

### Matlab (slower, for COCO evaluation)
- Compatible with general [Caffe](http://caffe.berkeleyvision.org/). Compile matcaffe. 
- Run `cd testing; get_model.sh` to retreive our latest MSCOCO model from our web server.
- Change the caffepath in the `config.m` and run `demo.m` for an example usage.

### Python
- `cd testing/python`
- `ipython notebook`
- Open `demo.ipynb` and execute the code

## Training

### Network Architecture
![Teaser?](https://github.com/ZheC/Multi-Person-Pose-Estimation/blob/master/readme/arch.png)

### Training Steps 
- Run `cd training; bash getData.sh` to obtain the COCO images in `dataset/COCO/images/`, keypoints annotations in `dataset/COCO/annotations/` and [COCO official toolbox](https://github.com/pdollar/coco) in `dataset/COCO/coco/`. 
- Run `getANNO.m` in matlab to convert the annotation format from json to mat in `dataset/COCO/mat/`.
- Run `genCOCOMask.m` in matlab to obatin the mask images for unlabeled person. You can use 'parfor' in matlab to speed up the code.
- Run `genJSON('COCO')` to generate a json file in `dataset/COCO/json/` folder. The json files contain raw informations needed for training.
- Run `python genLMDB.py` to generate your LMDB. (You can also download our LMDB for the COCO dataset (189GB file) by: `bash get_lmdb.sh`)
- Download our modified caffe: [caffe_train](https://github.com/CMU-Perceptual-Computing-Lab/caffe_train). Compile pycaffe. It will be merged with caffe_rtpose (for testing) soon.
- Run `python setLayers.py --exp 1` to generate the prototxt and shell file for training.
- Download [VGG-19 model](https://gist.github.com/ksimonyan/3785162f95cd2d5fee77), we use it to initialize the first 10 layers for training.
- Run `bash train_pose.sh 0,1` (generated by setLayers.py) to start the training with two gpus. 

## Related repository
- Our new C++ library [openPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose)
- CVPR'16, [Convolutional Pose Machines](https://github.com/shihenw/convolutional-pose-machines-release)
- [Pytorch version of the code](https://github.com/tensorboy/pytorch_Realtime_Multi-Person_Pose_Estimation)
## Citation
Please cite the paper in your publications if it helps your research:

    
    
    @inproceedings{cao2017realtime,
      author = {Zhe Cao and Tomas Simon and Shih-En Wei and Yaser Sheikh},
      booktitle = {CVPR},
      title = {Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields},
      year = {2017}
      }
	  
    @inproceedings{wei2016cpm,
      author = {Shih-En Wei and Varun Ramakrishna and Takeo Kanade and Yaser Sheikh},
      booktitle = {CVPR},
      title = {Convolutional pose machines},
      year = {2016}
      }
