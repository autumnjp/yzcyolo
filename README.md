# yzcyolo
This project collects and labels data sets for possible foreign bodies (such as hair, plastic, worms, etc.) in prepared vegetables, and uses the current mainstream target detection model
Training was carried out to realize the efficient detection of foreign bodies.
Python, Pytorch framework, OpenCV, tqdm, Yolov7 model
Data set preparation (data annotation, data preprocessing), model training, evaluation, and visual presentation of results.
![yzc1](https://github.com/user-attachments/assets/66b8edfe-3404-4cf1-a84c-c5f22c82a9ee)
![yzc2](https://github.com/user-attachments/assets/d1970fc7-df30-4bd3-88dd-adb1f600556d)

## 所需环境
torch==1.2.0    
为了使用amp混合精度，推荐使用torch1.7.1以上的版本。
## 训练步骤
**1. 数据集的准备** 
**本文使用VOC格式进行训练，训练前需要自己制作好数据集**    
训练前将标签文件放在VOCdevkit文件夹下的VOCyzc文件夹下的Annotation中。   
训练前将图片文件放在VOCdevkit文件夹下的VOCyzc文件夹下的JPEGImages中。   

**2. 数据集的处理**  
在完成数据集的摆放之后，我们需要利用voc_annotation.py获得训练用的yzc_train.txt和yzc_val.txt。   
修改voc_annotation.py里面的参数。第一次训练可以仅修改classes_path，classes_path用于指向检测类别所对应的txt。   
训练自己的数据集时，可以自己建立一个cls_classes.txt，里面写自己所需要区分的类别。   
model_data/cls_classes.txt文件内容为：      
```python
cat
dog
...
```
修改voc_annotation.py中的classes_path，使其对应cls_classes.txt，并运行voc_annotation.py。  

**3. 开始网络训练**  
**训练的参数较多，均在train.py中，大家可以在下载库后仔细看注释，其中最重要的部分依然是train.py里的classes_path。**  
**classes_path用于指向检测类别所对应的txt，这个txt和voc_annotation.py里面的txt一样！训练自己的数据集必须要修改！**  
修改完classes_path后就可以运行train.py开始训练了，在训练多个epoch后，权值会生成在logs文件夹中。  
```python train.py --cuda 0```

**4. 训练结果预测**  
训练结果预测需要用到两个文件，分别是yolo.py和predict.py。在yolo.py里面修改model_path以及classes_path。  
**model_path指向训练好的权值文件，在logs文件夹里。  
classes_path指向检测类别所对应的txt。**  
完成修改后就可以运行predict.py进行检测了。运行后输入图片路径即可检测。  
···python predict.py ---image_path```
