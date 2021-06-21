# Final Approach = Approach 1 + Approach 2 (This repo) 

Note: all approaches stated at the end of this readme

```
cd yolo-coco
wget https://pjreddie.com/media/files/yolov3.weights
cd ..
python3 yolo_video.py --input highway_01.mp4 --output highway_01_out.mp4 --yolo yolo-coco
```

Pros:
1. Handled hard shadows via Approach 2
2. Used minimum object size; far away objects are not considered via Approach 1

To run the repo: use `tf2.3.0`


# Approaches

### Approach 1:
#### Opencv + BG_substraction
ref: [link](https://github.innominds.com/gustavogino/Vehicle-Counter) (I translated the code)
 
Pros:

1. Very fast - almost realtime
2. Small objects are neglected (intended work because of random smaller detections via bg substraction)

Cons:
1. Fails when there are hard shadow in the frame
2. If a smaller car is present in the hard shadow of large truck then the whole truck + car = 1 vehicle

To address the above cons from Approach 1, I have used another repo which uses Yolo for vehicle detection

### Approach 2:
#### Yolo and centroid calculation from last 10 frames
ref: [link](https://github.com/guptavasu1213/Yolo-Vehicle-Counter)

Pros:
1. Uses deep learning, so is better at detecting vehicles even if there are hard shadows
2. Calculates centroid of last 10 frames and hence maintains correct count

Cons:
1. As it uses yolo, it is little slower than opencv approach
2. vehicles very far away in the frame are also counted, due to which count can get wrong sometimes


To address above cons, I simply added capabilities of Approach 1 into Approach 2 to make it more efficient.

