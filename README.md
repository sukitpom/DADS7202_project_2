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
2. Yolov5l unfreeze model และใช้ weight ที่ผ่าน pretrain 
3. Yolov5l Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และใช้ weight ที่ผ่าน pretrain 
4. Yolov5l Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และให้ Model ทำการปรับ Weight เอง
5. Yolov5l Freeze  10 layer แรกและใช้ weight ที่ผ่าน pretrain  
6. Yolov5s Freeze  10 layer แรกและใช้ weight ที่ผ่าน pretrain  


# 2. What is Yolov5?
The object detection method YOLO, which stands for "You Only Look Once," divide images into a grid structure. In the grid, each cell is in charge of finding objects within of it. Due to its accuracy and speed, YOLO is one of the most well-known object detection algorithms.

# 3. Code Detail

# 4. Result
1. Yolov5l unfreeze และ ปรับ Weightเอง <br>
<img src="pic/yolov5l_W_False_F_False_PR_curve.png" alt="drawing" align ="center" width ="400">

2. Yolov5l unfreeze model และใช้ weight ที่ผ่าน pretrain  <br>
<img src="pic/yolov5l_W_True_F_False_PR_curve.png" alt="drawing" align ="center" width ="400">

3. Yolov5l Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และใช้ weight ที่ผ่าน pretrain  
<img src="pic/yolov5l_W_True_F_True_PR_curve.png" alt="drawing" align ="center" width ="400">

4. Yolov5l Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และให้ Model ทำการปรับ Weight เอง <br>
<img src="pic/yolov5l_W_False_F_True_PR_curve.png" alt="drawing" align ="center" width ="400">   

5. Yolov5l Freeze  10 layer แรกและใช้ weight ที่ผ่าน pretrain  
<img src="pic/yolov5l_W_True_F10_True_PR_curve.png" alt="drawing" align ="center" width ="400">   


# 5. Summary

# Reference

[Yolov5]([https://](https://github.com/ultralytics/yolov5))

[C3 model ]([https://](https://arxiv.org/abs/1812.04920))
