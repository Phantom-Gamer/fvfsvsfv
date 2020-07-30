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

## Prerequisites and Setup

You will need these following to run this project:

 - Openvino 2019.R3
 - Python 3
 
*STEP 1:* 
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
 
*STEP 2:*
Now your intel Openvino is ready you will need to download Models required for this Project.

Navigate to 
