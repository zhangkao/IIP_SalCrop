# IIP_UAVSal_Saliency

It is a re-implementation code for the UAVSal model. 

Related Project
* Kao Zhang, Zhenzhong Chen, Shan Liu. A Spatial-Temporal Recurrent Neural Network for Video Saliency Prediction. IEEE Transactions on Image Processing (TIP), vol. 30, pp. 572-587, 2021. <br />
Github: https://github.com/zhangkao/IIP_STRNN_Saliency

* Kao Zhang, Zhenzhong Chen. Video Saliency Prediction Based on Spatial-Temporal Two-Stream Network. IEEE Transactions on Circuits and Systems for Video Technology (TCSVT), vol. 29, no. 12, pp. 3544-3557, 2019. <br />
Github: https://github.com/zhangkao/IIP_TwoS_Saliency


## Installation 
### Environment:
The code was developed using Python 3.6+ & pytorch 1.4+ & CUDA 10.0+. There may be a problem related to software versions.
* Windows10/11 or Ubuntu20.04
* Anaconda latest, Python 
* CUDA, CUDNN

### Python requirements
You can try to create a new environment in anaconda, as follows

    *For GEFORCE RTX 10 series, such as GTX1080, xp, etc. (Pytorch 1.4.0~1.7.1, python=3.6~3.8)

        conda create -n uavsal python=3.8
        conda activate uavsal
        conda install pytorch==1.4.0 torchvision==0.5.0 cudatoolkit=10.1 -c pytorch
        pip install numpy hdf5storage h5py==2.10.0 scipy matplotlib opencv-python scikit-image torchsummary

    *For GEFORCE RTX 30 series, such as RTX3060, 3080, etc.
        
        conda create -n uavsal python=3.7
        conda activate uavsal
        conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cudatoolkit=11.0 -c pytorch
        pip install numpy hdf5storage h5py==2.10.0 scipy matplotlib opencv-python scikit-image torchsummary


### Pre-trained models
Download the pre-trained models and put the pre-trained model into the "weights" file.

* **UAVSal-UAV2** 
[OneDrive](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/ERHo7kkmKjlEmbw7p8zQ1BUBn54i6jn6dabTkzkwNO50FA?e=7PWhjB) (52M)
* **UAVSal-AVS1K** 
[OneDrive](https://whueducn-my.sharepoint.com/:u:/g/personal/zhangkao_whu_edu_cn/ERJkGY-zClhBpEqgOixdTNcBhF6EYnJPGvKUlhcflxttcg?e=PaIycZ) (52M)

### Train and Test

**The parameters**

* Please change the working directory: "dataDir" to your path in the "Demo_Test.py" and "Demo_Train_Test.py" files, like:

        dataDir = '/home/name/DataSet/'
        
* More parameters are in the "train" and "test" functions.
* Run the demo "Demo_Test.py" and "Demo_Train_Test.py" to test or train the model.

**The full training process:**


* We initialize the SRF-Net with the pretrained MobileNet V2 and fine-tune the model on SALICON dataset. Then we train the whole model on EyeTrackUAV2  and AVS1K, respectively.

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
