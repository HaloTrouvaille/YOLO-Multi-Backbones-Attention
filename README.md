# Introduction  
This Repository includes YOLOv3 with some lightweight backbones (***ShuffleNetV2, GhostNet***), some computer vision attention mechanism (***SE Block, CBAM Block, ECA Block***), pruning and quantization for GhostNet.
# Important Update
***2020.6.1   
(1) The best lightweight model——HuaWei GhostNet has been added as the YOLOv3 backbone! It is better than ShuffleNetV2. The result is as following.  
(2) Add Dorefa quantization method for arbitrary bit quantization! The result is as following.  
(3) And I delete the ShuffleNet and the attention mechanism. If you need these previous model or have any question, you can add my WeChat: ssswwwyyy111***
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
  python3 train.py --data data/visdrone.data --batch-size 16 --cfg cfg/ghostnet-yolov3-visdrone.cfg --img-size 640
```
3. Detect objects using the trained model (place the pictures or videos in the ***samples*** directory)    
```
  python3 detect.py --cfg cfg/ghostnet-yolov3-visdrone.cfg --weights weights/best.pt --data data/visdrone.data
```
4. Results:  
![most](https://github.com/HaloTrouvaille/YOLO-Multi-Backbones-Attention/blob/master/output/most.png)  
![car](https://github.com/HaloTrouvaille/YOLO-Multi-Backbones-Attention/blob/master/output/car.png)  
![airplane](https://github.com/HaloTrouvaille/YOLO-Multi-Backbones-Attention/blob/master/output/airplane.png)  
# Prune and Quantization 
1. If you want to quantize certain convolutional layer, you can just change the [convolutional] to [quan_convolutional] in cfg file. Then use following command  
```
  python3 train.py --data data/visdrone.data --batch-size 16 --cfg cfg/ghostnet-yolov3-visdrone.cfg --img-size 640
```
***2.For pruning, I will update the pruning method for GhostNet soon!!!***
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
- [ ] COCO datasets training
- [ ] Other detection strategies
- [ ] Other pruning strategies

