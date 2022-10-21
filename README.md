# IIP_SalCrop

SalCrop: Spatio-temporal Saliency Based Video Cropping

Related Project
* Kao Zhang, Zhenzhong Chen. Video Saliency Prediction Based on Spatial-Temporal Two-Stream Network. IEEE Transactions on Circuits and Systems for Video Technology (TCSVT), vol. 29, no. 12, pp. 3544-3557, 2019. <br />
Github: https://github.com/zhangkao/IIP_TwoS_Saliency

## Abstract
Video cropping is a key research task in video processing field. In this paper, a spatio-temporal saliency based video cropping framework (SalCrop) is introduced including four core modules: video scene detection module, video saliency prediction module, adaptive cropping module, and video codec module. It can automatically reframe videos in the desired aspect ratios. In addition, a large-scale video cropping dataset (VCD) is built for training and testing. Experiments on the VCD test dataset show that our SalCrop outperforms the state-of-the-art algorithms with high efficiency. Besides, a FFmpeg video filter is developed based on the framework, which can be widely used in different scenarios. A demo is available at: [https://mme.tencent.com/smartcontent/videoCrop](https://mme.tencent.com/smartcontent/videoCrop) (access token: test_token).


## System Overview 
The framework of SalCrop is shown in Figure 1. It contains four main modules:

* **Video Scene Detection module**, in which long videos are automatically split into short sequences with consecutive shots based on key frames;
* **Video Saliency Prediction module**, in which a lightweight two-stream network is proposed to find salient content in the frames;
* **Adaptive Cropping module**, which can automatically choose an optimal cropping strategy to reframe videos with continuous and steady viewpoint, depending on the distribution of salient targets/regions in different frames; 
* **Video Codec module** for video encoding and decoding.

![SalCrop-fig](https://github.com/zhangkao/IIP_SalCrop/tree/master/figs/fig1.png)

## Implementation Details and Results

**Dataset：** 

A large-scale video cropping dataset (VCD) is proposed, which consists of 300 videos with various categories and photographic styles selected from three public video saliency prediction datasets: [LEDOV](https://github.com/remega/LEDOV-eye-tracking-database), [AVS1K](http://cvteam.buaa.edu.cn/papers.html/), and [DIEM](https://thediemproject.wordpress.com/). There are five subsets, including 60 clips of animals, 100 clips of man-made objects, 110 clips of human beings, 10 clips of landscapes, and 20 clips of others. These videos vary in the number of frames and resolution. The dataset is divided into three parts randomly: 100 sequences for training, 50 sequences for validation and 50 sequences for testing.

![VCD-fig](https://github.com/zhangkao/IIP_SalCrop/tree/master/figs/fig2.png)

## Implementation Details:
Our SalCrop is implemented in Python 3.7 and Pytorch 1.5 environment with a single NVIDIA V100 GPU and 2.5 GHz Intel Xeon Platinum 8255C CPU. 

## Experiments:
We conduct subjective assessment experiments on the VCD test dataset with 21 participants to compare our SalCrop with two methods: Google AutoFlip \cite{Frey20AutoFlip} and Adobe AutoReframe \cite{Adobe22Automatically}. Five-level scale is used for evaluation, in which numbers 1 to 5 are used to indicate the quality from bad to excellent. Our SalCrop achieves better performance (3.9) than AutoFlip (2.6) and AutoReframe (3.4) with ultra-fast speed (about 200FPS ignoring  IO cost). In addition, the combination of sampling and interpolation operations can be used to further improve efficiency.

## Demonstration:
Taking a video and a target aspect ratio (default 9:16 for the demo) as inputs, SalCrop can automatically analyze the video content, develop an optimal cropping strategy, and generate a reframed output video. More demo videos can be found at [https://youtu.be/U5geNZq8pNo](https://youtu.be/U5geNZq8pNo).


**The training and testing datasets:**

* **Training dataset**: 
[SALICON(2015)](http://salicon.net/), 
[UAV2](https://www.mdpi.com/2504-446X/4/1/2/), and 
[AVS1K](http://cvteam.buaa.edu.cn/papers.html/)
* **Testing dataset**: 
[UAV2-TE](https://www.mdpi.com/2504-446X/4/1/2/) and
[AVS1K-TE](http://cvteam.buaa.edu.cn/papers.html/)


**The training and test data examples:**
* **Training data example**: 
[UAV2](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/ET1Fa3CqLyxCrpsCwF8gM-8BTJye0OLztTl5vigg-Kr7gw?e=iFMLga) (376M)
[AVS1K](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/EbxQR0fnsppEnVD4Y7SCELIBgYSuAjYct1stVXQcxAGivQ?e=6g5QOc) (147M)
* **Testing data example**:
[UAV2-TE](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/EaAkpNbZ0YxCtEKnLid4BpwBtWfm4KcrsM3qDmAn4jNX_A?e=jBd8Df) (483M)
[AVS1K-TE](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/EeHjqpW3aetAqRmtKt7UCU8BtZirn1PsfIhT8GgWRlPzPQ?e=WiyANH) (29M)




### Output
And it is easy to change the output format in our code.
* The results of video task is saved by ".mat"(uint8) formats.
* You can get the color visualization results based on the "Visualization Tools".
* You can evaluate the performance based on the "EvalScores Tools".
* You can get the parameter size of each component based on the "Getmodelsize Tools".


**Results**: [ALL](https://whueducn-my.sharepoint.com/:f:/g/personal/zhangkao_whu_edu_cn/EucCA9ArT1NIqpEokhDjzSMBivD86OFdKrtuzUvHw9UIJA?e=R9ofo9) (5.8G):

The model is trained using Adam optimizer with lr=0.0001 and weight_decay=0.00005    
* **Version V1** : 
[UAV2-TE](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/ET2r9UlJ4R1Dkc5eLIq_qr0BfwEy9VIXreb5zElzPAy9vQ?e=oMepX9) (707M)
[AVS1K-TE](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/EWjG4vOefPZItLWE0L1eGbkBAsHgVUsbK1AU6tbbXwWZNA?e=KAiTSQ) (1.8GM), 

The model is trained using Adam optimizer with lr=0.00001 and weight_decay=0.000005 
* **Version V2** : 
[UAV2-TE](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/EUuGfQaPiVFAi42YUnyzHzgBVyqhG2InQXKIyupJxUuEYw?e=wQodTB) (639M), 
[AVS1K-TE](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/EUsv8PA3gqdHldJZKMrTCGQBoA9c2_J29ifDkdBh--W_3g?e=qFD1Qa) (2.04G)

It can achieve faster speed (85FPS) with similar performance by slightly reducing the input size from original 360 x 640 pixels to 288 x 512 pixels
* **UAV2** : 
[weigths](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/EYU765b1XmxLrV2s7daghHwBF1US8eeCawWQJRgGONhKuQ?e=ix4cOa) (52M), 
[results](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/EWDU7TylkgVAnZcDNVctvsUBhKrxneMWOwqp7m_uFIU2-A?e=A8c1gM) (649M)


### Video Demo

A video demo is provided for comparison with State-of-the-art methods, including: [OneDrive](https://whueducn-my.sharepoint.com/:v:/g/personal/zhangkao_whu_edu_cn/ESCIRe02WSZPmKGjVD08PBUB_ChN9c67gppIt5ZUZ3m8ZA?e=Fb0mS6) (596M)
* DL based models: STRNN*, TwoS*, TASED*, UNISAL*
* non-DL based models: GBVSm, AWSD.


* The models fine-tuned on the corresponding dataset (UAV2 and AVS1K) are marked with *.
* After fine-tuning, the performance of these models improved significantly.
* The first four scenes are from the UAV2-TE dataset, the rest are from AVS1K-TE.

## Paper & Citation

If you use the UAVSal video saliency model, please cite the following paper: 
```
@article{zhang2022an,
  title={An Efficient Saliency Prediction Model for Unmanned Aerial Vehicle Video},
  author={Zhang, Kao and Chen, Zhenzhong and Li, Songnan and Liu, shan},
  journal={ISPRS Journal of Photogrammetry and Remote Sensing},
  volume={xxxx},
  pages={xxxx},
  year={2022}
}
```



## Contact
Kao ZHANG  <br />
Laboratory of Intelligent Information Processing (LabIIP)  <br />
Wuhan University, Wuhan, China.  <br />
Email: zhangkao@whu.edu.cn  <br />

Zhenzhong CHEN (Professor and Director) <br />
Laboratory of Intelligent Information Processing (LabIIP)  <br />
Wuhan University, Wuhan, China.  <br />
Email: zzchen@whu.edu.cn  <br />
Web: http://iip.whu.edu.cn/~zzchen/  <br />
