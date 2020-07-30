# Computer Pointer Controller using Intel OpenVino

In this project we will control the Mouse Pointer of User's Computer through Gaze Detection Model. This model estimates the position of the User Eyes and will move the Mouse accordingly.
 
We can supply the input via a Video file or User's Webcam.
 
You will be using the InferenceEngine API from Intel's OpenVino ToolKit to build the project. The Gaze Detection Model uses three parameters as input:
  
  - The head pose of User
  - The left eye image 
  - The right eye image
  
 To get these we need other three models which will help us supply the input to Gaze Detection Mode:
 
  - Face Detection Model
  - Head Pose Detection Model
  - Facial Landmarks Detection Model
  
  
## The Pipeline
We will have to coordinate the flow of data from the input, and then amongst the different models and finally to the mouse controller. The flow of data will look like this:

![pipeline](/images/pipeline.png)

## Directory Structure

![structure](/images/structure.png)



## Prerequisites and Setup

You will need these following to run this project:

 - Openvino 2019.R3
 - Python 3
 
 
## *STEP 1:* 

Register and download Intel Openvino from [here](https://software.intel.com/content/www/us/en/develop/tools/openvino-toolkit/choose-download.html) which will be compatible for your Platform. 
 
 After installation of Openvino run this command:
 
 ```
 I/P:
 "C:\Program Files (x86)\IntelSWTools\openvino_2019.3.334\bin\setupvars.bat"
 
 O/P:
 Python 3.8.0
 ECHO is off.
 PYTHONPATH=C:\Program Files (x86)\IntelSWTools\openvino_2019.3.334\deployment_tools\open_model_zoo\tools\accuracy_checker;C:\Program Files (x86)\IntelSWTools\openvino_2019.3.\python\python3.8;C:\Program Files (x86)\IntelSWTools\openvino_2019.3.334\python\python3;C:\Program Files (x86)\IntelSWTools\openvino_2019.3.334\deployment_tools\open_model_zoo\tool\accuracy_checker;C:\Program Files (x86)\IntelSWTools\openvino_2019.3.334\python\python3.8;C:\Program Files (x86)\IntelSWTools\openvino_2019.3.334\python\python3;
 [setupvars.bat] OpenVINO environment initialized
 ```
 This will initialize the Opevino Enviroment.
 
 Now for a Demo run goto demo folder and run a inbuilt Project of Openvino
 ```
 cd C:\Program Files (x86)\IntelSWTools\openvino_2019.3.334\deployment_tools\demo
 demo_squeezenet_download_convert_run.bat
 ```
 
 This will download a Model for you and show some output like this on your screen. (It takes some time for doing this)
 
 ![first_run](/images/output_openvino_first_run.png)
 
 This indicates that everything is OK on your System and Openvino is working properly!
 
 
## *STEP 2:*

Now your intel Openvino is ready you will need to download Models required for this Project.

Navigate to:
```
cd C:\Program Files (x86)\IntelSWTools\openvino_2019.3.334\deployment_tools\tools\model_downloader
```

and run the following commands:
```
python3 downloader.py --name gaze-estimation-adas-0002 
python3 downloader.py --name face-detection-adas-binary-0001  
python3 downloader.py --name head-pose-estimation-adas-0001  
python3 downloader.py --name landmarks-regression-retail-0009
```

This will download all the required Models for this Project.


## *STEP 3*:

Now just copy this folder where you want to inside your Computer.
Open Command Prompt there and run the following commands:

```
"C:\Program Files (x86)\IntelSWTools\openvino_2019.3.334\bin\setupvars.bat"

pip install -r requirements.txt 
```

Now this will initialize the OpenVino Enviroment for our Project and download the requiremnets mentioned in the file requirements.txt


## *Step 4:*

Goto src/ folder.

Now you can run this Project on CPU / GPU / FPGA / VPU / NCS 2 Stick

Hit:

```
python main.py -h
```

This will output the required arguments for main.py

Arguments:

-  -h  : Informantion about available commands
-  -fd : Path to Face Detection Model's xml file  **Required
-  -fl : Path of Facial landmarks Detection Model xml file  **Required
-  -hp : Path of Head Pose Estimation model's xml file  **Required
-  -ge : Path of Gaze Estimation model's xml file  **Required
-  -i  : If youn want to use Camera for input specify the Camera or if you want to use Video file specify path to file  **Required
-  -d  : Device to use CPU, GPU, FPGA,  **Optional
-  -pt : If you want to specify threshold  **Optional
-  -flag : Specify the flags from fd, fl, hp, ge to visualize the output of corresponding model  **Optional


## *STEP 5:*

To run this Project you can use the following commands according to the device:


- CPU
```
python <project_file.py directory> -fd <Face detection model name directory> -fl <Facial landmark detection model name directory> -hp <head pose estimation model name directory> -ge <Gaze estimation model name directory> -i <input video directory> -d CPU
```

- GPU
```
python <project_file.py directory> -fd <Face detection model name directory> -fl <Facial landmark detection model name directory> -hp <head pose estimation model name directory> -ge <Gaze estimation model name directory> -i <input video directory> -d GPU
```

- FPGA
```
python <project_file.py directory> -fd <Face detection model name directory> -fl <Facial landmark detection model name directory> -hp <head pose estimation model name directory> -ge <Gaze estimation model name directory> -i <input video directory> -d HETERO:FPGA,CPU
```

- NCS 2 Stick
```
python <project_file.py directory> -fd <Face detection model name directory> -fl <Facial landmark detection model name directory> -hp <head pose estimation model name directory> -ge <Gaze estimation model name directory> -i <input video directory> -d MYRIAD
```

## Benchmarks

|Model|	Type|Load Time in seconds|
|---|---|---|
|Face Detection Model| FP32 | 570 ms|
|Head Pose Detection Model | FP32 |375 ms|
|Facial landmarks Detection Model | FP32 | 270 ms|
|Gaze Detection Model | FP32 |  340 ms|


 - Total loading time: 1600 milliseconds
 - Total Inference time :  90 seconds
 - FPS : 0.7 frames/sec
 
 ## Edge Cases
 
- If there are more than one face detected in the frame then model takes the first detected face for controlling the mouse pointer

- This project can be utilized to identify and alert Students if they miss attention from Online Classes or identify and alert Sleeping drivers
