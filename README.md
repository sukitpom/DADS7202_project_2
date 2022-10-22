# <p align="center"> One Piece Character Detection </p>

by Capybarista Team

# Output:
![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/1.%20output.JPG)

# Step of work:
- 1. Raw data: Following figure is example of Raw Data

![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/2.%20Raw%20data.jpg)
 
- 2. Highlight Data Profiling

RFM model and imbalance data

![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/10.jpg)


Respone type vs K-MEAN result 

![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/5.%20KMEAN%20vs%20Respone.JPG)

Respone type vs key parameter

![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/6.JPG)
![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/7.JPG)

- Create new parameter to use in prediction model that is shown in following

![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/3.%20Parameter.JPG)

- Feature selection
                             
![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/4.%20Feature%20selection.JPG)

- Highest score

![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/8.JPG)
![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/9.JPG)

- Conclusion

![alt](https://github.com/NattapongTH/NattapongTH-6310422089_BADS7105/blob/main/Homework%2008%20%E2%80%93%20Campaign%20Response%20Model/Photo/11.jpg)

# Capybarista Group <p> *Object Detection One Piece* </p>

# 1. Overview 
Data  จำนวน 1182 รูป ประกอบก้วย 9 คลาสดังนี้
- Brook         92  รูป
- Chopper       204 รูป
- Franky        175 รูป
- Luffy         364 รูป
- Nami          205 รูป
- Robin         217 รูป
- Sanji         171 รูป
- Usopp         271 รูป
- Zoro          263 รูป
  
แบ่งเป็น Train:Test:Split   70 : 20 : 10

กระบวนการ Create Dataset ด้วย Roboflow มีดังนี้
1. PREPROCESSING
    - Auto-Orient: Applied
    - Resize: Stretch to 416xv416
    - Tile: 2 rows x 2 columns
2. AUGMENTATIONS
    - Outputs per training example: 3
    - Flip: Horizontal, Vertical
    - Crop: 0% Minimum Zoom, 20% Maximum Zoom
    - Rotation: Between -31° and +31°
    - Brightness: Between -25% and +25%
    - Blur: Up to 2px
  
รูปภาพที่ผ่านการ AUGMENTATIONS มีจำนวนทั้งสิ้น 11232 รูป แบ่งได้เป็น
1. Train      จำนวน 9756 รูป ( 87% )
2. Validation จำนวน 984  รูป (  8% )
3. Test       จำนวน 528  รูป (  5% ) 

Model ที่ใช้ในการทดสอบคือ Yolov5s และ Yolov5l
แบ่งการทดสอบดังนี้
1. Yolov5l unfreeze model และให้ Model ทำการปรับ Weight เอง
2. Yolov5l unfreeze model และใช้ weight ที่ผ่าน pretrain (yolov5l.pt)
3. Yolov5l Freeze   model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และใช้ weight ที่ผ่าน pretrain (yolov5l.pt)
4. Yolov5l Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และให้ Model ทำการปรับ Weight เอง
5. Yolov5l Freeze  10 layer แรกและใช้ weight ที่ผ่าน pretrain  
6. Yolov5s Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และใช้ weight ที่ผ่าน pretrain  (yolov5s.pt)


# 2. What is Yolov5?
The object detection method YOLO, which stands for "You Only Look Once," divide images into a grid structure. In the grid, each cell is in charge of finding objects within of it. Due to its accuracy and speed, YOLO is one of the most well-known object detection algorithms.

# 3. Code Detail

# 4. Result
## PR Curve
1. Yolov5l unfreeze และไม่ใช้ weight ที่ผ่าน pretrain <br>
<img src="pic/yolov5l_W_False_F_False_PR_curve.png" alt="drawing" align ="center" width ="400">

2. Yolov5l unfreeze model และใช้ weight ที่ผ่าน pretrain  <br>
<img src="pic/yolov5l_W_True_F_False_PR_curve.png" alt="drawing" align ="center" width ="400">

3. Yolov5l Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และใช้ weight ที่ผ่าน pretrain  
<img src="pic/yolov5l_W_True_F_True_PR_curve.png" alt="drawing" align ="center" width ="400">

4. Yolov5l Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และไม่ใช้ weight ที่ผ่าน pretrain <br>
<img src="pic/yolov5l_W_False_F_True_PR_curve.png" alt="drawing" align ="center" width ="400">   

5. Yolov5l Freeze  backbone 10 layer แรกและไม่ใช้ weight ที่ผ่าน pretrain  
<img src="pic/yolov5l_W_True_F10_True_PR_curve.png" alt="drawing" align ="center" width ="400">   

6. Yolov5s Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inferenceและใช้ weight ที่ผ่าน pretrain 



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
