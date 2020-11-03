# Introduction  
This Repository includes YOLOv3 with some lightweight backbones (***ShuffleNetV2, GhostNet, VoVNet***), some computer vision attention mechanism (***SE Block, CBAM Block, ECA Block***), pruning,quantization and distillation for GhostNet.
# Important Update
***2020.6.1***     
(1) The best lightweight model——HuaWei GhostNet has been added as the YOLOv3 backbone! It is better than ShuffleNetV2. The result for visdrone dataset is as following.  
(2) Add Dorefa quantization method for arbitrary bit quantization! The result for visdrone dataset is as following.  
(3) And I delete the ShuffleNet and the attention mechanism.   
***2020.6.24***    
(1) Add pruning according to NetworkSlimming.  
(2) Add distillation for higher mAP after pruning.  
(3) Add Imagenet pretraining model for GhostNet.  
***2020.9.26***  
(1) Add VoVNet as the backbone. The result is excellent.

| Model | Params | FPS | mAP |
| ----- | ----- | ----- |----- |
| GhostNet+YOLOv3 | 23.49M | 62.5 | 35.1 |
| Pruned Model+Distillation | 5.81M | 76.9 | 34.3 |
| Pruned Model+INT8 | 5.81M | 75.1 | 34 |
| YOLOv5s | 7.27M | - | 32.7 |
| YOLOv5x | 88.5M | - | 41.8 |  
| VoVNet | 42.8M | 28.9 | 42.7 |  

***Attention : Single GPU will be better***  
***If you need previous attention model or have any question, you can add my WeChat: AutrefoisLethe***
# Environment  
* python 3.7  
* pytorch >= 1.1.0  
* opencv-python  
# Datasets
* Oxfordhand datasets (1 class, including human's hand)  
https://pan.baidu.com/s/1ZYKXMEvNef41MdG1NgWYiQ     (extract code: 00rw) 
* Visdrone Remote datasets (10 classes, including pedestrian, car, bus, etc)  
https://pan.baidu.com/s/1JzJ6APRym8K64taZgcDZfQ     (extract code: xyil)
* Bdd100K datasets (10 classes, including motor, train, traffic light, etc)  
https://pan.baidu.com/s/1dBrKEdy92Mxqg-JiyrVjkQ     (extract code: lm4p)
* Dior datasets (20 classes, including airplane, airport, bridge, etc)  
https://pan.baidu.com/s/1Fc-zJtHy-6iIewvsKWPDnA     (extract code: k2js) 

# Usage
1. Download the datasets, place them in the ***data*** directory    
2. Train the models by using following command (change the model structure by changing the cfg file)  
```
  python3 train.py --data data/visdrone.data --batch-size 16 --cfg cfg/ghost-yolov3-visdrone.cfg --img-size 640
```
3. Detect objects using the trained model (place the pictures or videos in the ***samples*** directory)    
```
  python3 detect.py --cfg cfg/ghostnet-yolov3-visdrone.cfg --weights weights/best.pt --data data/visdrone.data
```
4. Results:  
![most](https://github.com/HaloTrouvaille/YOLO-Multi-Backbones-Attention/blob/master/output/most.png)  
![car](https://github.com/HaloTrouvaille/YOLO-Multi-Backbones-Attention/blob/master/output/car.png)  
![airplane](https://github.com/HaloTrouvaille/YOLO-Multi-Backbones-Attention/blob/master/output/airplane.png)  
# Pruning and Quantization 
## Pruning
First of all, execute sparse training.  
```
python3 train.py --data data/visdrone.data --batch-size 4 --cfg cfg/ghost-yolov3-visdrone.cfg --img-size 640 --epochs 300  --device 3 -sr --s 0.0001
```
Then change cfg and weights in normal_prune.py then use following command  
```
python normal_prune.py
```
After obtaining pruned.cfg and corresponding weights file, you can fine-tune the pruned model via following command  
```
python3 train.py --data data/visdrone.data --batch-size 4 --cfg pruned.cfg --img-size 640 --epochs 300  --device 3 --weights weights/xxx.weighs
```

## Quantization
If you want to quantize certain convolutional layer, you can just change the [convolutional] to [quan_convolutional] in cfg file. Then use following command  
```
  python3 train.py --data data/visdrone.data --batch-size 16 --cfg cfg/ghostnet-yolov3-visdrone.cfg --img-size 640
```

# Experiment Result for Changing YOLOv3 Backbone
## ShuffleNetV2 + Two Scales Detection(YOLO Detector)
### Using Oxfordhand datasets
| Model | Params | Model Size | mAP |
| ----- | ----- | ----- |----- |
| ShuffleNetV2 1x | 3.57M | 13.89MB | 51.2 |
| ShuffleNetV2 1.5x | 5.07M | 19.55MB | 56.4 |
| YOLOv3-tiny | 8.67M | 33.1MB | 60.3 |
### Using Visdrone datasets(Incomplete training)
| Model | Params | Model Size | mAP |
| ----- | ----- | ----- |----- |
| ShuffleNetV2 1x | 3.59M | 13.99MB | 10.2 |
| ShuffleNetV2 1.5x | 5.09M | 19.63MB | 11 |
| YOLOv3-tiny | 8.69M | 33.9MB | 3.3 |
# Experiment Result for Attention Mechanism
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

 
# TODO
- [x] ShuffleNetV2 backbone
- [x] HuaWei GhostNet backbone 
- [x] ImageNet pretraining
- [x] COCO datasets training
- [ ] Other detection strategies
- [ ] Other pruning strategies


