# <p align="center"> One Piece Character Detection </p>

by Capybarista Team
<p align="center" width="100%">
    <img width="80%" src="https://github.com/NattapongTH/DADS7202_project_2/blob/main/pic/Header.jpg"> </span>



# Brief Result:

- Model comparison with mAP@0.5 score and Running time
   - roboflow (Default) - (0.7)
   - Yolov5l - Weight False Freeze False (0.709 / 5.36 hr)
   - Yolov5l - Weight True Freeze False (0.787 / 5.35 hr)
   - Yolov5l - Weight False Freeze True (0.002 / 2.42 hr)
   - Yolov5l - Weight True Freeze True (0.066 / 2.43 hr)
   - Yolov5l - Weight True Freeze 10 (0.673 / 3.22 hr)
   - Yolov5s - Weight True Freeze True (ยังไม่เสร็จ)

- The Best Model (Highest score) = Yolov5l - Weight True Freeze False (Unfreeze Model + Adjust weight from pre-train result)
- Alternative model (Balance between score and running time) = Yolov5l - Weight True Freeze 10

# Introduction:
- Object detection: Object detection is a computer vision technique that allows us to identify and locate objects in an image or video. 
With this kind of identification and localization, object detection can be used to count objects in a scene and determine and track their precise locations, all while accurately labeling them.
The comparison between image classification, object detection and instance segmentation shown in below.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/NattapongTH/DADS7202_project_2/blob/main/pic/Picture1.png"> </span>

from: Standford University 2016 winter lectures CS231n Fei-Fei Li & Andrej Karpathy & Justin Johnson

- roboflow: Roboflow is a computer vision platform that allows users to build computer vision models faster and more accurately through the provision of better data collection, preprocessing, 
and model training techniques. Roboflow allows users to upload custom datasets, draw annotations, modify image orientations, resize images, modify image contrast and perform data augmentation. 
It can also be used to train models.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/NattapongTH/DADS7202_project_2/blob/main/pic/roboflow.jpg"> </span>

Image augmentation is an efficacious technique when we don’t have an ample amount of data for training a deep learning model. 
Our team do Image augmentation with roboflow (due to time limitation, we set criteria of image augmentation as default of roboflow). Following figure is image augmentation options in roboflow.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/NattapongTH/DADS7202_project_2/blob/main/pic/augmentation-options.png"> </span>
     
Step of roboflow for One Piece Character Detection Project
1. Upload photo to roboflow
2. Label One Piece Character in all photo.
3. Image preprocessing & Image augmentation
4. Train.
5. Deploy.

<p align="center" width="100%">
    <img width="80%" src="https://github.com/NattapongTH/DADS7202_project_2/blob/main/pic/roboflow%20step.png"> </span>

Image source and detail of roboflow tutorial --> https://blog.streamlit.io/how-to-use-roboflow-and-streamlit-to-visualize-object-detection-output/

# Our project in roboflow:
- Project Link: https://app.roboflow.com/dl-yjboe/dads7202_hw2
- Total image = 1182 picture (Number of photo for each character shown below. Some picture have multi-character)
- Number of photo after image augmentation = 11232
- Train-Test Split = 70 : 20 : 10 --> After Image augmentation, Train : Validation : Test : 87% : 8% : 5%
- Other setting shown in below

<p align="center" width="100%">
    <img width="80%" src="https://github.com/NattapongTH/DADS7202_project_2/blob/main/pic/Number%20of%20character.jpg"> </span>
<p align="center" width="100%">
    <img width="80%" src="https://github.com/NattapongTH/DADS7202_project_2/blob/main/pic/roboflow%20setting.jpg"> </span>


# roboflow's outcome:
- mAP for Train / Validation / Test of all charactor = 71% / 68% / 70%

<p align="center" width="100%">
    <img width="80%" src="https://github.com/NattapongTH/DADS7202_project_2/blob/main/pic/roboflow%20score.png"> </span>

However, roboflow have some limitation about tuning. Next step, team will use jupyter in colab to adjust hyperparameter.

---------------------------------------------------

# Our project in jupyter-colab:
- Project Link: https://colab.research.google.com/drive/1hfHihyPVFt18axpft3brB-uG-jAQ9OoM?usp=sharing#scrollTo=ii8qC1HDUzZ6
มีของ yolov5s จะแยกหรือร่วม colab
- 6 Comparison base on batch-size = 16 and 100 epochs (default)
   - Yolov5l - Weight False Freeze False (unfreeze layer + No update weight via pretrain step)
   - Yolov5l - Weight True Freeze False (unfreeze layer + Allow to update weight via pretrain step)
   - Yolov5l - Weight False Freeze True (Freeze all layer (except output layer) + No update weight via pretrain step)
   - Yolov5l - Weight True Freeze True (Freeze all layer (except output layer) + Allow to update weight via pretrain step)
   - Yolov5l - Weight True Freeze 10 (Freeze backbone = 10 layer + No update weight via pretrain step)
   - Yolov5s - Weight True Freeze True (Freeze all layer (except output layer) + Allow to update weight via pretrain step + Change to Yolov5s) (ยังไม่เสร็จ)

# mAP@0.5 score from Jupyter-colab:
   - Yolov5l - Weight False Freeze False = 0.709

<p align="center" width="100%">
    <img width="80%" src="pic/yolov5l_W_False_F_False_PR_curve.png"> </span>

   - Yolov5l - Weight True Freeze False = 0.787

<p align="center" width="100%">
    <img width="80%" src="pic/yolov5l_W_True_F_False_PR_curve.png"> </span>

   - Yolov5l - Weight False Freeze True = 0.002

<p align="center" width="100%">
    <img width="80%" src="pic/yolov5l_W_False_F_True_PR_curve.png"> </span>

   - Yolov5l - Weight True Freeze True = 0.066

<p align="center" width="100%">
    <img width="80%" src="pic/yolov5l_W_True_F_True_PR_curve.png"> </span>

   - Yolov5l - Weight True Freeze 10 = 0.673 

<p align="center" width="100%">
    <img width="80%" src="pic/yolov5l_W_True_F10_True_PR_curve.png"> </span>

   - Yolov5s - Weight True Freeze True (ยังไม่เสร็จ)


# Jupyter-colab's outcome:
- The best score model = Yolov5l - Weight True Freeze False, 0.787
- However, running time is high. The running time of each model shown below

<p align="center" width="100%">
    <img width="80%" src="https://github.com/NattapongTH/DADS7202_project_2/blob/main/pic/Running%20time.png"> </span>

- Alternative model (Balance between score and running time) = Yolov5l - Weight True Freeze 10 --> Score drop ~15% but save time ~40% 


---------------------------------------------------




---------------------------------------------------

# 2. What is Yolov5?
The object detection method YOLO, which stands for "You Only Look Once," divide images into a grid structure. In the grid, each cell is in charge of finding objects within of it. Due to its accuracy and speed, YOLO is one of the most well-known object detection algorithms.




## mAP@0.5 ของโมเดลรูปแบบต่าง ๆ<br>
<img src="pic/chart_PR_curve.png " alt="drawing" align ="center" width ="400">  <br> 

โมเดลที่ให้ผลลัพธ์ดีที่สุด 3 อันดับแรกคือ โมเดลที่ 2 3 และ 5 มีค่า mAP@0.5 อยู่ที่ 0.787 0.709 และ 0.ตามลำดับ ส่วนโมเดล 3 และ 4 ที่มีการ Freeze ทั้งโมเดลจะให้ผลลัพธ์ที่ตรงข้ามกันอย่างสิ้นเชิง ซึ่งค่า mAP@0.5 ที่ได้ในแต่ละโมเดลมีความสอดคล้องกับ Precision-Recall Curve โดยโมเดลที่มีค่า mAP@0.5 มากเส้นโค้ง Precision-Recall ก็จะมาค่าเข้าใกล้ 1 เมื่อพิจารณา mAP@0.5 ในแต่ละ Epoch ของโมเดลที่ 1 2 และ 5 จะพบว่าค่า mAP@0.5 จะมีอัตราการเปลี่ยนแปลงที่ไม่แตกต่างจากเดิมมากนักตั้งแต่ Epoch 80 เป็นต้นไป ในส่วนของเวลาที่ใช้ในการประมวลผลของแต่ละโมเดลจะเป็นดังต่อไปนี้<br>

<img src="pic/cls_log_loss.png " alt="drawing" align ="center" width ="400">  <br> 

โมเดลที่ใช้เวลานานที่สุดคือ โมเดลที่ 1 2 5 ซึ่งใช้เวลา 5.355 5.353 และ 3.222 ชั่วโมงตามลำดับ


# 5. Summary
จากการทดลองทั้ง 6 โมเดลพบว่าโมเดลที่ให้ค่า mAP@0.5 ดีที่สุดคือ โมเดล 2 ที่ Unfreeze Model และใช้ Weight ที่ผ่าน Pre-train ซึ่งให้ผลลัพธ์ที่ดีกว่า โมเดล 1 ที่ Unfreeze Model และไม่ใช้ Weight ที่ผ่าน Pre-train ซึ่งทั้ง 2 โมเดลนี้ให้ค่า mAP@0.5 ที่แตกต่างกันมาก ในขณะที่ใช้เวลาในการ Train ไม่แตกต่างกันอย่างมีนัยสำคัญ แต่เมื่อพิจารณาโมเดลที่ 5 กับโมเดลที่ 2 พบว่าค่า mAP@0.5 ของโมเดล 5 ให้ผลลัพธ์ไม่ต่างอย่างมีนัยสำคัญกับโมเดลที่ 1 แต่กลับใช้เวลาในการ Train ที่น้อยกว่าโมเดลที่ 1 มาก ส่วนโมเดลที่ 3 และ 4 ที่มีการ Freeze ทั้งโมเดลยกเว้น Inference Layer จะให้ผลลัพธ์ที่ไม่เหมาะสม เนื่องการเป็นส่วนของ Head กับ Neck ที่เกี่ยวข้องกับการทำนายผลลัพธ์ ซึ่งไม่ใช่ส่วนของ Feature Extraction จึงทำให้โมเดลไม่มีการเปลี่ยนแปลง Back Propagation ในส่วนของการทำนายผลให้สอดคล้องกับ Dataset ชุดใหม่ 

# 6. Future Work
- ทำการ unfreeze ในส่วนของ Head และ Neck ตามลำดับเพื่อเปรียบเทียบผลลัพธ์กับการ unfreez พร้อมกัน
- เปรียบเทียบผลลัพธ์ของโมเดลที่ 1 2 5 กับ yoloV5 ที่เป็น verion s m x ว่าผลลัพธ์จะยังเป็นเหมือนเดิมเหรือไม่
- เพิ่ม Dataset เพื่อทดสอบดูว่าความแม่นยำเพิ่มขึ้นหรือไม่ 

# Reference

[Yolov5]([https://](https://github.com/ultralytics/yolov5))

[C3 model ]([https://](https://arxiv.org/abs/1812.04920))
