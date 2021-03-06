# Mask_Detection
The Face Mask Detection System relies on the concepts of Computer vision and Deep learning using 
OpenCV and Tensorflow / Keras in order to detect face masks in still images as well as in real-time
video streams. So this system can be used in real-time applications that require face mask detection 
for safety purposes due to the Covid-19 virus outbreak. This project can be combined with integrated
systems for application in airports, railway stations, offices, schools and public places to ensure
that public safety guidelines are followed.

# Dataset
The dataset used can be downloaded here - [Click to Download ](https://drive.google.com/file/d/1NxxBwcPipK28TwKlpVKZSRXkvO-Twi_V/view?usp=sharing)

This dataset consists of 3835 images that fall into two categories:

  - with_mask: 1916 images
   
  - without_mask: 1919 images

The photos used were actual photos of faces wearing masks. Pictures were collected from the following sources:

  - [x] Bing Search API [(See Python script)](https://github.com/chandrikadeb7/Face-Mask-Detection/blob/master/search.py)
  - [x] Kaggle datasets
  - [x] RMFD dataset[(See here)](https://github.com/X-zhangyang/Real-World-Masked-Face-Dataset)

# Model 
The face mask detector did not use any masking image data set. The model is accurate, and since I used
**ResNet50 Architecture** without layers classified as the base model for extracting features from the images,
It is also computationally efficient and thus makes it easy to deploy the model to embedded systems.

- **ResNet50** is a pre-trained Keras model with the feature of letting you use weights that are already
    calibrated to make predictions. In this case, I'm using weights from Imagenet and the network is ResNet50.
      
      Include_top = False 
      
    It allows you to extract features by removing the last dense layers. This allows me to control form output and input.
   
      input_tensor = input (format = (224, 224, 3))
      base_model = ResNet50 (include_top = False, weights = 'imagenet', input_tensor = input_tensor) 
      
- The starting point is very useful since i already have weights used to classify images but since
  I'm using them in a brand new dataset, adjustments are needed. My goal is to build a model with high accuracy
  in its rating. This indicates how to use previously trained model layers. I actually have several parameters
  due to the number of ResNet50 layers but we have calibration weights.

- I choose **freeze** these layers (as much as I can) so these values don't change, this way saving time and computational cost.
  In this case, I am **freezing** all ResNet50 layers. The way to do this in Keras is by using:
  
      For the layer in base_model.layers:
         layer.trainable = false   
         
- Later on, I needed to link the previously trained layers with the new layers for the model.
  I used the **GlobalAveragePooling2D** layer to link the dimensions of the previous layers to the new layers.
  Using only **GlobalAveragePool2D layer, dense layer with relu layer and dense layer with softmax**,
  I can perform closing the form and start the classification procedure.
  
- [x] **Optimization Methods**: I tested this over 100 epochs using **RMSprop** to get the result.

- [x] **You can download my model here:[(click here)](https://drive.google.com/file/d/1VdBF9ZC6WGJ6dfSiH3rOEMzDFhaMf4pb/view?usp=sharing)**


# How to Use
To use this project on your system, follow these steps:

1- Clone this repository onto your system by typing the following command on your Command Prompt:

    git clone https://github.com/dodo295/Mask_Detection

followed by:

    cd Mask_Detection
    
 2- Ensure that you have all the required libraries used in all files.
   In case a library is missing, download it using pip, by typing this on your Command Prompt:
      
    pip install 'library name'

Replace 'library-name' by the name of the library to be downloaded.

  
 3- **Train your Model** by typing the following commands on your Command Prompt:
      
    python loader.py Train_Model.py
    
 - [x] **For face detction using Haarcascade Algorithm**   
   - Run Haarcascade_FaceMaskImage.py by typing the following command on your Command Prompt:
    
         python Mask_Detection_Image.py --image Your_test.jpg
    
    - To open your webcam and discover if there is a mask or not! Writing:

          python Haarcascade_FaceMaskWebcam.py 
 - [x] **For face detction using YOLOv3 Algorithm**         
   - image input

         python YOLOFaceMask.py --image samples/1.jpg --output-dir outputs/
   - video input

         python YOLOFaceMask.py --video samples/your_video.mp4 --output-dir outputs/
   - webcam

         python yYOLOFaceMask.py --src 0 --output-dir outputs/ 
   
# Results
- I got **100% accuracy in the training set** and **99.74% verification set** with 100 epochs.

![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/Accuracy%20plot.png)![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/Loss%20plot.png)


- Debate over the use of freezing continues in the previously tested model.
It reduces calculation time, reduces overuse but reduces accuracy.When the new data set is very
different from the data set used for training, it may be necessary to use more layers for modification.


- When selecting hyperparameters, it is important to impart learning to use a low learning rate to take
advantage of ready-made model weights. This selection as an optimizer option (SGD, Adam, RMSprop)
will affect the number of durations required to successfully obtain a trained model.

# Examples
The first step in implement my model is face detection in an image or frame of a video stream
and there are a lot of techniques that can be used in face detection. Here I used two of these techniques
- **haarcascde deep learning algorithm**

![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/haarcascade_Outputs/Output1.png)
![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/haarcascade_Outputs/Output2.png)

![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/haarcascade_Outputs/Output3.png)
![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/haarcascade_Outputs/Output4.png)
- **YOLOv3 algorithm**
I performed face detection using [this project](https://github.com/sthanhng/yoloface) as my guide, so thank you very much.

**YOLOv3**(You Only Look Once) is a modern, real-time object detection algorithm.
  You must download the pre-trained YOLOv3 weights file trained on [WIDER FACE: A Face Detection Benchmark](http://shuoyang1213.me/WIDERFACE/)
  dataset from this [link](https://drive.google.com/file/d/1xYasjU52whXMLT5MtF7RCPQkV66993oR/view) and place it in the project directory.

![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/YOLOv3_Outputs/2_yoloface.jpg)
![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/YOLOv3_Outputs/3_yoloface.jpg)

![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/YOLOv3_Outputs/8_yoloface.jpg)
![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/YOLOv3_Outputs/5_yoloface.jpg)

![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/YOLOv3_Outputs/4_yoloface.jpg)
![grab-landing-page](https://github.com/dodo295/Mask_Detection/blob/main/YOLOv3_Outputs/9_yoloface.jpg)
