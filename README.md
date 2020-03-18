# Introduction  
This Repository includes YOLOv3 with some lightweight backbones (***ShuffleNetV2, MobileNet***), some computer vision attention mechanism (***SE Block, CBAM Block, ECA Block***), pruning and quantization (reference to my senior's Repository https://github.com/coldlarry/YOLOv3-complete-pruning)
# Enviroment
* python 3.7  
* pytorch >= 1.1.0  
* opencv-python  
# Datasets
* Oxfordhand datasets (1 class, including human's hand)
* Visdrone Remote datasets (10 classes, including pedestrian, car, bus, etc)
* Bdd100K datasets (10 classes, including motor, train, traffic light, etc)
* Dior datasets (20 classes, including airplane, airport, bridge, etc)
# Usage
1. Download the datasets, place them in the ***data*** directory    
2. Train the models by using following command (change the model structure by changing the cfg file)  
```
  python3 train.py --data data/oxfordhand.data --batch-size 16 --cfg cfg/yolov3-shufflenetv2-hand.cfg --img-size 608
```
3. Detect objects using the trained model (place the pictures or videos in the ***samples*** directory)    
```
  python3 detect.py --cfg cfg/yolov3-shufflenetv2-hand.cfg --weights weights/backup100.pt --data data/oxfordhand.data
```
# Changing YOLOv3 Backbone
## ShuffleNetV2 + Two Scales Detection(YOLO Detector)
### Using Oxfordhand datasets
| Model | Params | Model Size | mAP |
| ----- | ----- | ----- |----- |
| ShuffleNetV2 1x | 3.57M | 13.89MB | 51.2 |
| ShuffleNetV2 1.5x | 5.07M | 19.55MB | 56.4 |
| YOLOv3-tiny | 8.67M | 33.1MB | 60.3 |
### Using Visdrone datasets
| Model | Params | Model Size | mAP |
| ----- | ----- | ----- |----- |
| ShuffleNetV2 1x |  |  |  |
| ShuffleNetV2 1.5x | 5.09M |  | 11 |
| YOLOv3-tiny | 8.69M |  | 3.3 |
# Attention Mechanism
### Based on YOLOv3-tiny
SE Block paper : https://arxiv.org/abs/1709.01507  
CBAM Block paper : https://arxiv.org/abs/1807.06521  
ECA Block paper : https://arxiv.org/abs/1910.03151  
| Model | Params | mAP |
| ----- | ----- | ----- |
| YOLOv3-tiny | 8.67M | 60.3 |
| YOLOv3-tiny + SE | 8.933M | 62.3 |
| YOLOv3-tiny + CBAM | 8.81M | 62.7 |
| YOLOv3-tiny + ECA | 8.67M | 62.6 |
# Prune and Quantization 
Based on my senior's Repository, reference to https://github.com/coldlarry/YOLOv3-complete-pruning  
# TODO
- [x] ShuffleNetV2 backbone
- [ ] MobileNet backbone 
- [ ] COCO datasets training
- [ ] Other detection strategies
- [ ] Other pruning strategies

