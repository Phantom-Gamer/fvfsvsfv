# Computer Pointer Controller using Intel OpenVino

In this project we will control the Mouse Pointer of User's Computer through Gaze Detection Model. This model estimates the position of the User Eyes and will move the Mouse accordingly.
 
We can supply the input via a Video file or User's Webcam.
 
You will be using the InferenceEngine API from Intel's OpenVino ToolKit to build the project. The Gaze Detection Model uses three parameters as input:
  
  - The head pose of User
  - The left eye image 
  - The right eye image
