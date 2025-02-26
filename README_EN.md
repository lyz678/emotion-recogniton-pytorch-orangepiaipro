# Emotion-recogniton-pytorch
This project focuses on recognizing human emotions from facial expressions using deep learning techniques implemented in PyTorch. The model is trained on the FER-2013 dataset, a widely-used dataset in the field of facial expression recognition, achieving 81.3% accuracy.
In addition, we used Ascendcl to deploy the model to the Orange Pi AI Pro with Huawei Ascend 310B NPU to achieve real-time expression detection on mobile devices.
![Image text](http://www.orangepi.cn/img/aipro/aipro-18.png)

# Install
```bash
git clone https://github.com/lyz678/Emotion-recogniton-pytorch.git  # clone
cd Emotion-recogniton-pytorch
pip install -r requirements.txt  # install
```

# FER2013 Dataset
- Dataset from [https://www.kaggle.com/c/challenges-in-representation-learning-facial-expression-recognition-challenge/data](https://www.kaggle.com/datasets/deadskull7/fer2013)
Image Properties: 48 x 48 pixels (2304 bytes)
labels: 0=Angry, 1=Disgust, 2=Fear, 3=Happy, 4=Sad, 5=Surprise, 6=Neutral
The training set consists of 28,709 examples. The public test set consists of 3,589 examples. The private test set consists of another 3,589 examples.
- download the dataset(fer2013.csv) then put it in the "fer2013" folder
  
```bash
cd fer2013
pip install kaggle
kaggle datasets download -d deadskull7/fer2013
unzip fer2013
```

# Train and Eval model
- python train_emotion_classifier.py --model MiniXception --bs 128 --lr 0.01


# .pth to .onnx
```bash
python pt2onnx.py
```

# Real time video
```bash
python run_on_cpu.py
```
![Image text](https://github.com/lyz678/Emotion-recogniton-pytorch/blob/main/result/demo1.jpg)
![Image text](https://github.com/lyz678/Emotion-recogniton-pytorch/blob/main/result/demo2.jpg)


# plot confusion matrix
- python plot_fer2013_confusion_matrix.py --model MiniXception --bs 128
![Image text](https://github.com/lyz678/Emotion-recogniton-pytorch/blob/main/result/ConfusionMatrix.jpg)

# fer2013 Accurary      
- Model：    miniXception ;        test accuracy：  65% <Br/>
- Model：   Resnet18 ;      test accuracy：  82%

# run on Orange Pi AI Pro (Ascend310B NPU)

- download the run_on_Ascend310B file to Orange Pi AI Pro

  
```bash
cd run_on_Ascend310B
atc --model=miniXception.sim.onnx --framework=5 --output=miniXception.sim --input_format=NCHW --input_shape="input.1:1,1,48,48" --log=error --soc_version=Ascend310B1 #.onnx to .om
python run_om.py
```
![Image text](https://github.com/lyz678/Emotion-recogniton-pytorch/blob/main/result/demo3.JPG)



# referrence
https://github.com/otaha178/Emotion-recognition
