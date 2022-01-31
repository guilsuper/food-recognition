<h1 align="center">🍔🍟🍗 Food Analysis with YOLOv5 🍞🍖🍕</h1>

<p align="center">
   <a href="./LICENSE"><img src="https://img.shields.io/github/license/Naereen/StrapDown.js.svg" alt="MIT" /></a>

 <a href="https://github.com/lannguyen0910/food-detection-yolov5/stargazers">
 <img src="https://img.shields.io/github/stars/lannguyen0910/food-detection-yolov5?style=flat-square" alt="Stars"/>
 </a>
 <a href="https://github.com/lannguyen0910/food-detection-yolov5/fork">
 <img src="https://img.shields.io/github/forks/lannguyen0910/food-detection-yolov5.svg?style=flat-square" alt="Forks"/>
 </a>
 <img src="https://visitor-badge.laobi.icu/badge?page_id=lannguyen0910.food-detection-yolov5" alt="visitors" />
 
 <a><img  src="./demo/pipeline.png"></a>
  <br>
</p>


<p align="center">
  <a href="https://www.codefactor.io/repository/github/lannguyen0910/food-detection-yolov5/overview/master"><img src="https://www.codefactor.io/repository/github/lannguyen0910/food-detection-yolov5/badge/master?s=9716a4eb0076053fa36e0d967bba5161b85b8fb5" alt="CodeFactor" /></a>
  <a href="https://www.python.org/"><img src="https://img.shields.io/badge/Made%20with-Python-1f425f.svg" alt="Python" /></a>
 
 <a href="https://github.com/lannguyen0910/food-detection-yolov5/issues">
<img src="https://img.shields.io/github/issues/lannguyen0910/food-detection-yolov5?style=flat-square" alt="Issues"/>
</a>
<a href="https://github.com/lannguyen0910/food-detection-yolov5/pulls">
<img src="https://img.shields.io/github/issues-pr/lannguyen0910/food-detection-yolov5?style=flat-square" alt="Pull Requests"/>
</a>
</p>

<!--
## 🌳 **Folder Structure**

<details>
  <summary><strong>Details</strong></summary>

```
food-detection-yolov5
|
│   app.py                    # Flask server
|   modules.py                # inference stage, export result files, csv,...
|
└───api      
│   └─── ...
│   └─── api.py               # make request, update db
│   └─── secret.py            # get reponse 
|
└───model                     
│   └─── ...
│   └─── detect.py            # image detection
│   └─── video_detect.py      # video detection
|
└───static
│   └─── ...
│   └─── assets               # contain upload files, detection files
│   └─── css                  # custom css files, bootstrap
│   └─── js
|       └─── ...
│       └─── client.js        # custom js for templates
│       └─── chart.js         # nutrients analysys with charts
|
└───templates
│   └─── ...  
│   └─── index.html           # upload files' page
│   └─── url.html             # input URLs' page    
```
</details> -->
   

<details open> <summary><strong>Dev logs</strong></summary>
<strong><i>[31/01/2022]</i></strong> Big refactor - Update to new YOLOv5 version 5, 6. Can load checkpoints from original repo now 🤞.<br>
 <strong><i>[26/12/2021]</i></strong> Update app on Android 🤞 <br>
 <strong><i>[12/09/2021]</i></strong> Update all features to the web app 🤞 <br>
 <strong><i>[16/07/2021]</i></strong> All trained checkpoints on custom data have been lost. Now use pretrained models on COCO for inference. 
</details>

🚨 **UPDATE**:
- WandB yolov5 training visualization (4 versions): <a href="https://wandb.ai/lannguyen/food-detection-yolov5"><img src="https://raw.githubusercontent.com/wandb/assets/main/wandb-github-badge-gradient.svg" alt="WandB"></a> 
- The accuracy is very high on our custom datasets now (90 classes), will update new datasets in the future (for diversity).
- [Food app](https://github.com/lannguyen0910/food-detection-yolov5/tree/food-android) branch (Not update yet).
- Best current [weights](https://drive.google.com/drive/folders/15PlXWkFheuBxJOYkwm9iS_aZCcr8L0A7?usp=sharing). 

<!-- - Visualize [test images](https://drive.google.com/drive/folders/1Af7Ilg99fI8p3T7BM5cFo5lJz_xY-Jxt?usp=sharing) with best current weights. -->

## 📔  **Notebook**
- For inference, use this notebook to run the web app [![Notebook](https://colab.research.google.com/assets/colab-badge.svg)](https://drive.google.com/file/d/1CGEtC65kvoZ-4tcqzeknGrbERvb0beuU/view?usp=sharing)
- For training, refer to this notebook i use for training [![Notebook](https://colab.research.google.com/assets/colab-badge.svg)](https://drive.google.com/file/d/1SywGfyfj3SVrE7VAAl3CshB9s3o8WRXL/view?usp=sharing)
 ## 🌟 **Inference on local machine (GPU or CPU)**
- Clone the repo.
```
git clone https://github.com/lannguyen0910/food-detection-yolov5
cd food-detection-yolov5/
```
- Install dependencies.
```
pip install -r requirements.txt
pip uninstall opencv-python-headless==4.5.5.62
pip install opencv-python-headless==4.5.2.52
```

- (Optional) Install [ffmpeg](http://ffmpeg.org/). Rebuild ```ffmpeg``` with ```OpenCV``` to display MP4 video in browser: [link](https://stackoverflow.com/questions/31040746/cant-open-video-using-opencv). Or check out the colab notebook bellow: [![Notebook](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1JMH9vwvxmWy72yXxV2-niRUTW_J3PlQM?usp=sharing)
```
sudo apt-get install ffmpeg
```

- Start the app. Safe to run in insecure connection ```http``` on localhost. You can generate SSL certificate to run the app in ```https```.
```
run.bat
```

- Switch from ```CPU``` to ```GPU``` for faster inference, change 4 yolov5 config files in ```utilities/configs``` 
```
gpu: True
```
## 🌟 **Export Torchscript / Onnx / Bin-Param for [ncnn](https://github.com/Tencent/ncnn) usage**
- Example usage:
```
pip install onnx>=1.9.0 onnx-simplifier>=0.3.6
python tools/export.py --weights yolov5s_best.pt --imgsz 640 --include onnx
```

```
python tools/export.py --weights yolov5s_best.pt --imgsz 320 320 --include torchscript
```

- Open notebook and follow the instructions [![Notebook](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1nf0lLo6e2nMAt_AtDNoHmeXzdAB9kxsj?usp=sharing)

## 🌟 **Datasets**
- Datasets: [detection-dataset](https://drive.google.com/drive/folders/14rJclN97hZqe6bmGkTjnvPaDBBIF4v5w?usp=sharing) (merged 2 datasets) & [classification-dataset](https://drive.google.com/drive/folders/11PH1ZF3ZCMKDQvxrblBA-Zy02iWgM4lq?usp=sharing) (MAFood121)

## 🌟 **Dataset details**
<details>
<summary>To train the food detection model, we survey the following datasets:</summary>
  
  - <a href="https://storage.googleapis.com/openimages/web/index.html">Open Images V6-Food</a>: Open Images V6 is a huge dataset from Google for Computer Vision tasks. To solve our problem, we extracted from a large dataset on food related labels. The extracted set includes 18 labels with more than 20,000 images.
  - <a href="http://foodcam.mobi/dataset.html">School Lunch Dataset</a>: includes 3940 photos of a lunch of Japanese high school students, taken at the same frontal angle with the goal of assessing student nutrition. Labels consist of coordinates and types of dishes are attached and divided into 21 different dishes, in the dataset there is also a label "Other Foods" if the dishes do not belong to the remaining 20 dishes.
  - <a href="https://drive.google.com/drive/folders/1PLrsJBS1EtJLY6RpEriASTfQ5WRlPQAt?usp=sharing">Vietnamese Food</a>: a self-collected dataset on Vietnamese dishes, including 10 simple dishes of our country such as: Pho, Com Tam, Hu Tieu, Banh Mi,... Each category has about 20-30 images, divided 80-20 for training and evaluation.
  
We aggregate all the above datasets to proceed training. Dishes that appear in different sets will be grouped into one to avoid duplication. After aggregating, a large data set of 60,305 images with 44 different foods from all regions of the world.
<br>
  
In addition, we find that if we expand the problem to include classification, the dataset will increase significantly. Therefore, to further enhance the diversity of dishes, we collect additional datasets to additionally train a classification model:
  - <a href="http://www.ub.edu/cvub/mafood121/">MAFood-121</a>: consisting of 21,175 training image samples. The dishes are selected from the top 11 most popular cuisines in the world according to Google Trends statistics, these cuisines come from many countries around the world, especially Vietnam. For each type of cuisine, 11 typical traditional dishes are selected. The dataset has a total of 121 different types of dishes, each belonging to at least 1 of 10 food categories: Bread, Eggs, Fried, Meat, Noodles, Rice, Seafood, Soup, Dumplings, and Vegetables . 85% of the images are used for training and the remaining 15% for evaluation.
  - <a href="https://data.vision.ee.ethz.ch/cvl/datasets_extra/food-101/">Food-101</a>: includes 101 different types of dishes, with 101,000 sets of photos. For each dish, 250 images were used as test images and the remaining 750 images were used for training. The training images in this set still have a lot of noise, sometimes the colors are too sharp or some of the data samples are mislabeled, these noises are intentional by the author (mentioned in the study).
  
We also perform the aggregation of the two data sets above into one. The new set includes <b>93,748 training images</b> and <b>26,825 evaluation images</b> with a total of <b>180 different dishes</b>. It can be seen that the number of dishes has increased significantly, if the model detects a dish labeled "Other Foods", the classification model will be applied to this dish and classified again.
</details>

## 🌟 **YOLOv5 models**
We use <b>4 YOLOv5 versions (s, m, l and x)</b> and their pre-trained weights to train on our problem. The model's source code is inherited from the <a href="https://github.com/ultralytics/yolov5">Ultralytics</a> source code repo, and the training and data processing steps are reinstalled by us using Pytorch. When training, data augmentation methods are applied to minimize the model's easy overfit.
<br>

## 🌟 **Server**
<details>
<summary>Implementation details</summary>
   
The two functions: ```get_prediction``` and ```get_video_prediction``` are two inference functions for images and videos. Implemented in ```modules.py```, where the image detection process (get_prediction) will call the Edamam API to get nutritional information in the food. We also save nutritional information in csv files in the folder ```/static/csv```.
<br>

We provide the user with the ability to customize the threshold of confidence and iou so that the user can find a suitable threshold for the input image. In order not to have to rerun the whole model every time these parameters are changed, when the image is sent from the client, the server will perform a ```perceptual hash``` encryption algorithm to encrypt the image and using that resulting string to name the image when saving to the server. This helps when the client sends an image whose encoding already exists in the database, the server will only post-process the previously predicted result without having to re-execute the prediction.
<br>

In addition, the team also saved the models as ```global variables```. When starting Flask Server, the model will be initialized only once. Only when there is a change in model selection, this variable will be reinitialized, otherwise the model will not be reinitialized when there are new image queries, this will somewhat reduce the processing time.
</details>
   
## 🌟 **Additional Methods**
<details>
<summary>To increase the variety of dishes, we apply a classification model:</summary>
<br>
After testing and observing, we use a simple and effective model: EfficientNet. EfficientNet is proposed by Google and is one of the state-of-the-art models in this classification problem, and efficiency is also guaranteed. We apply the EfficientNet model source code from rwightman, we select the <b>EfficientNet-B4</b> version for retraining on the aggregated dataset. This model is used as an additional improvement to the YOLOv5 model in case the model detects a dish labeled as "Other Foods", only then EfficientNet is applied to predict the label again for this dish.
  
</details>
<details>
<summary>To increase the accuracy of the algorithm, we use the ensemble models technique:</summary>
<br>
  
For each image, models with different versions are used to predict, the results are then aggregated using the "<b>weighted box fusion</b>" method to give the final result.
  
</details>
<details>
<summary>To increase users' interactivity with the application:</summary>
<br>
  
When a dish is predicted, we provide more information about the nutritional level of that dish to the user. This information is queried from the application's database, which will be periodically updated from the Edamam API - an API that allows querying the nutrition of a dish by dish name. When doing prediction, the nutrition information will be saved along with the dish name under <b>CSV</b> format. We then fetch the CSV file on the client site to proceed drawing nutritrion statistics chart using <a href="https://github.com/chartjs/Chart.js">Chart.js</a> library. There are a total of 2 chart types, which appear when the user clicks on that chart type.
</details>

## 🍱 **Sample Results**
<p float="left">
  <img src="demo/2.jpg" width="100%" /> 
  <img src="demo/1.jpg" width="100%" />
  <img src="demo/3.jpg" width="100%" />
  <img src="demo/4.jpg" width="100%" />
  <img src="demo/5.jpg" width="100%" /> 
  <img src="demo/6.jpg" width="100%" />
</p>

## 📝 **Appendix**
<details open>
<summary>mAP of each model. Visualization details at: <a href="https://wandb.ai/lannguyen/food-detection-yolov5"><img src="https://raw.githubusercontent.com/wandb/assets/main/wandb-github-badge-gradient.svg" alt="WandB"></a></summary>
  <br>
 
- Valset: 

| Models  | Image Size | Epochs    | mAP@0.5  | mAP@0.5:0.95 |
| ------- | :--------: | :------: | :------: | :----------: | 
| YOLOv5s |  640x640   |  172        | 94.36 |   72.08      |  
| YOLOv5m |  640x640   |    112      | 93.01  |   71.88      |  
| YOLOv5l |  640x640   |      118    |  96.55  |   78.75      | 
| YOLOv5x |  640x640   |    62     |  83.56  |    60.11     |

---

<!-- - Testset (old version):

| Models  | Image Size | mAPsmall | mAPmedium | mAPlarge | mAP@0.5:0.95 |
| ------- | :--------: | :------: | :-------: | :------: | :----------: |
| YOLOv5s |  640x640   |   6.3    |   28.4    |   30.3   |     30.5     |
| YOLOv5m |  640x640   |   7.5    |   28.7    |   30.6   |     30.9     |
| YOLOv5l |  640x640   |   38.4   |   46.8    |   57.9   |     57.5     |
| YOLOv5x |  640x640   |   55.0   |   48.9    |   59.8   |     55.1     | -->
</details>

We conclude that the learned models are quite good compared to such huge data with such a variety of dishes, and their complexity is also guaranteed to be suitable for practical applications. We show that the system is scalable and has high practical significance for the people of Vietnam in particular and the world in general.
<br>

## 💡 **Further Improvements**
- We have yet to solve the problem of messy data labels (with one sample labeling the dish, another labeling the ingredients of the dish) causing the score to be not really accurate. You can try to train on other food datasets for better experience!

- Feel free to make a contribution to the project by pulling a request or making an issue.

## 📙 **Credits**
- YOLOv5 official repo: https://github.com/ultralytics/yolov5.
- Object detection's custom template: https://github.com/kaylode/custom-template/tree/detection.
- Base code for android app: https://github.com/cmdbug/YOLOv5_NCNN.
- Ncnn by Tencent: https://github.com/Tencent/ncnn
- Edamam API: https://developer.edamam.com/food-database-api-docs.
- Chart.js: https://github.com/chartjs/Chart.js.
