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
### a、训练数据集
1. 数据集的准备   
**本文使用VOC格式进行训练，训练前需要准背好数据集，解压后放在根目录**  

2. 数据集的处理   
修改voc_annotation.py里面的annotation_mode=2，运行voc_annotation.py生成根目录下的2007_train.txt和2007_val.txt。   

3. 开始网络训练   
train.py的默认参数用于训练VOC数据集，直接运行train.py即可开始训练。   

4. 训练结果预测   
训练结果预测需要用到两个文件，分别是yolo.py和predict.py。我们首先需要去yolo.py里面修改model_path以及classes_path，这两个参数必须要修改。   
**model_path指向训练好的权值文件，在logs文件夹里。   
classes_path指向检测类别所对应的txt。**   
完成修改后就可以运行predict.py进行检测了。运行后输入图片路径即可检测。   
