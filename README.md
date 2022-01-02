# Object-Detection
Object detection and localization for custom dataset

The task is to train a model for object detection and localization on a dataset with 2 classes: 
  1. Car
  2. Person

The dataset is annotated with coco format. 

## Documentation

### Assumptions
1. The annotations provided are accurate. 
2. The classes are balanced so that the model can learn and train itself on both the classes equally. 


### Approach
1. I decided to use YOLOv5(insert link) since it is already trained on the coco dataset. Also it is fast and easy to setup.
2. I converted the annotations to yolo format. Further details are present in the jupyter notebook ().
3. I then divided the data into train and validation with a 85% and 15% split respectively.
4. There are three kinds of yolov5 models - small, medium and large. I used the pretrained weights provided here(insert link) and used the dataset to finetune all the three kinds of yolov5 models.
5. Since my gpu was not working with the pytorch version, I used my cpu to train the small and medium model which took about 2 hrs and 4hrs respectively (link for the jupyter-notebook). For the large model I used google colab to train the model on gpu which took about ~1.5 hrs. (link for the google colab notebook)

### Metrics
1. While training the yolov5 network, we can link our runtime to wandb.ai and it keeps a track of all the epochs. It gives us various metrics such as precision, recall, mAP and losses for both training and validation.
2. I have attached imaged of all the metrics in the results folder.

### Other artifacts
1. The comparison between the three yolo networks shows that the large network performs the best. But the drawback is that it takes the most time to train. 




