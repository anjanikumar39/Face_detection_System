# Face_detection_System
Face Detection System (By Anjani Kumar)
Step 1: Setup environment
Open VS (visual studio code), select folder where you want to implement, 
Create Azure Function New project with HTTP Trigger.
Then open terminal in VS code then install these packages.

Install Necessary packages:

![image](https://github.com/user-attachments/assets/52c9dbd5-eed1-4f14-ab6f-2ec2d2afd30d)

Step 2: Logic Inside
Copy the code from my function_app.py and paste it in your VS code function_app.py in system.
A)Load Haar Cascade Classifier:
The function uses OpenCV's pre-trained Haar cascade (haarcascade_frontalface_default.xml) for face detection. It checks if the classifier is loaded correctly; otherwise, it returns an error message.
B)Convert Image Bytes to NumPy Array:
The input image, provided as raw bytes, is converted into a NumPy array using np.frombuffer.
C)Decode Image:
The NumPy array is decoded into an OpenCV-compatible image format using cv2.imdecode. If decoding fails, it returns an error indicating invalid image content or format.
D)Convert to Grayscale:
The image is converted to grayscale (cv2.COLOR_BGR2GRAY) as the Haar cascade works better with grayscale images.
E)Detect Faces:
The detectMultiScale method scans the grayscale image to detect faces based on the following parameters:
scaleFactor=1.1: Specifies how much the image size is reduced at each image scale.
minNeighbors=5: Defines how many neighbors a rectangle should have to considered a face.
minSize=(30, 30): Sets the minimum size of detected objects (faces).
F)Return Detection Result:
The function checks the length of the detected faces array:
Returns True if one or more faces are detected.
Returns False if no faces are detected.

Step 3: HTTP Trigger

Route Definition:
The function is exposed as an HTTP endpoint (/facedetection) using the @app.route decorator. It accepts anonymous requests (auth_level=func.AuthLevel.ANONYMOUS).
GET Request Handling:
Serves an HTML form for face detection.
The form allows users to submit an image URL for processing.
POST Request Handling:
Extract Image URL: Retrieves the image_url submitted via the form.
Validate Image URL: Ensures the URL is provided and fetches the image using requests.get. 
If fetching fails, an appropriate error is returned.
Face Detection:
The detect_faces function processes the fetched image bytes to determine if faces are present.
The result (Yes or No) is included in a dynamically generated HTML response.
Error Handling:
Logs errors and returns a user-friendly message if an exception occurs during processing.
HTML Responses:
Both the form and result pages are styled and branded with a Singularium logo.
Users can submit a new image URL for analysis after viewing results.
Deploy: Deploy it in Azure Function for 24*7 running system.

Example:
Open Image in Chrome with face and right click on copy image address.

![image](https://github.com/user-attachments/assets/33a7ad02-2d3c-461c-92dd-a2323769eb7f)

Paste this URL in blank space in facedetectionsystem and you will get the result True or False.

![image](https://github.com/user-attachments/assets/7efe416f-2702-4fd3-86a3-f1dda58d25e5)

After Result:

![image](https://github.com/user-attachments/assets/64c87b40-36da-4154-a127-cab45fa09e1f)



