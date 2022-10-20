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
1. Yolov5l unfreeze model และ ให้ Model ทำการปรับ Weight เอง
2. Yolov5l Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และใช้ weight ที่ผ่าน pretrain 
3. Yolov5l Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference และใช้ weight ที่ผ่าน pretrain  
4. Yolov5s Freeze  model ทั้งหมดยกเว้น Layer สุดท้ายสำหรับใช้ Inference

# 2. What is Yolov5?

# 3. Code Detail

# 4. Result

# 5. Summary

# Reference

[Yolov5]([https://](https://github.com/ultralytics/yolov5))

[C3 model ]([https://](https://arxiv.org/abs/1812.04920))
