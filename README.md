# Object-Detection
Object detection and localization for custom dataset

The task is to train a model for object detection and localization on a dataset with 2 classes: 
  1. Car
  2. Person

The dataset is annotated with coco format. 

## Documentation


The file structure is: 
```bash
├── eagleView
│   ├── eagle_data
│       │──images
│          │──train
│          │──validation
│       │──labels
│          │──train
│          │──validation
│
│   ├── yolov5 (cloned repo)
│       ├── contains the download weights
│   
├── Object Detection.ipynb
└── data.yaml

```



### Approach
1. I decided to use [YOLOv5](https://github.com/ultralytics/yolov5) since it is already trained on the coco dataset. Also it is fast and easy to setup.
2. I converted the annotations to yolo format. Further details are present in the jupyter notebook [here](https://github.com/bansalraghav/Object-Detection/blob/main/Object%20Detection.ipynb).
3. I then divided the data into train and validation with a 85% and 15% split respectively.
4. There are three kinds of yolov5 models - small, medium and large. I used the pretrained weights provided [here](https://github.com/ultralytics/yolov5/releases) and used the dataset to finetune all the three kinds of yolov5 models. I have trained all the models for a maximum of 10 epochs.
5. Since my gpu was not working with the required pytorch version, I used my cpu to train the small and medium model which took about 2 hrs and 4hrs respectively (https://github.com/bansalraghav/Object-Detection/blob/main/Object%20Detection.ipynb). 
6. For the large model I used google colab to train the model on gpu which took about ~1.5 hrs. (https://github.com/bansalraghav/Object-Detection/blob/main/YOLOv5_large.ipynb)
7. For training the yolo model, we need to define 4 details in a yaml file. These are:
  - train images path
  - validation images path 
  - nc (number of classes)
  - names (class names)
8. There are 2 yaml files which I have provided. The [data.yaml](https://github.com/bansalraghav/Object-Detection/blob/main/data.yaml) contains the configurations which I used to train the small and medium models locally whereas the [colab_data.yaml](https://github.com/bansalraghav/Object-Detection/blob/main/colab_data.yaml) contains the config I used to train the large model in google colab.

### Assumptions
1. The annotations provided are accurate. 
2. The classes are balanced so that the model can learn and train itself on both the classes equally. 

### Metrics
1. While training the yolov5 network, we can link our runtime to wandb.ai and it keeps a track of all the epochs. It gives us various metrics such as precision, recall, mAP and losses for both training and validation.
2. I have attached imaged of all the metrics in the [Results](https://github.com/bansalraghav/Object-Detection/tree/main/Results) folder.
3. In the confusion matrix we can see that for the medium and large model, the false positive rate is less for the "car" category as compared to the small model. For the "person" category the false positive rate is high for all three models.

### Other artifacts
1. The comparison between the three yolo networks shows that the large network performs the best. But the drawback is that it takes the most time to train. 

### Conclusion
1. YOLOv5 is a SOTA model which is easy to setup and quick to train. The only drawback would be to convert our custom annotations to yolo format but that also can be done with relative ease. Using the dataset which was provided to me, I was able to generate a mAP of 0.7 for the large and medium model which is good considering the fact that the model was only trained for 10 epochs with a batch size of 8. 

### Recommendations
1. If we are to train the large model for more epochs and a large batch size, we may get slightly better results.
2. Hyperparameter tuning can also lead to better results.
