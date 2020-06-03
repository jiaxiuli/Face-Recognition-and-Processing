# Face-Recognition-and-Processing
This project is currently developing. At present, users can upload a local image, or link the image by url, then the image information will be sent to the API by url or base 64 code. The faces on the image will be detected, through the JSON data received from API, information of age, emotion, gender, beauty, skin status, smile, glass, and other properties of each face of every person on the image will be displayed.

## The overall effect:
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/overall.png)

## Upload local image and detect:
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/overall%20upload.png)

## link image by URL:
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/overall%20url.png)

## Main idea:
### 1. Allow users upload image files and covert the image file to base 64 code.
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/upload%20file.png)

### 2. Call API with the base 64 code as one of the parameters.
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/file%20call%20api.png)

### 3. Process the received JSON data. 
This process includes abstrcting the information of age, emotion, gender.... what's more, the faces on the image should be marked with a rectangle, and clip down the facial parts from the whole image.
#### So, there are two things we should do, first, process the whole image, mark the face and clip down.
I set up a Canvas to do it, set the background image of the canvas is the uploaded image, and draw some rectangle based on the coordinate information received from API.
This is the API returned coordinate data called face_rectangle:
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/face_rectangle.png)

Set up Canvas and reset the size of the image, becuase the size of each uploaded image is not fixed, so we have to reset the size of the image to make sure the image displayed is not too big or too small, as well as the correct position.
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/reset_size.png)

Then we need reset the size of the Canvas the same as the image, otherwise, the image will be stretched.
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/reset_position1.png)

Then draw the rectangle on the Canvas. However, the returned coordinate information is based on the original size of the image, since we changed the size of the image, so the coordination should be changed proportionably. Fianlly, draw every rectangle on the canvas with a for loop.
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/reset_position2.png)

#### Second, process the attributes data.
This is the returned attributes information:
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/attributes.png)
Before display the text of these attributes, I suppose the screenshot of the face should be displayed first. So, create a new Image object, set the url or base 64 code as img.src, and call the function drawImage() to clip down a specific area of the whole image.
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/clip.png)
then is the attributes text:
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/text.png)
So far, this is the display of one face, one person, to display that for every body in the picture, use a for loop to make a traversal and append the element to the div.

### Process the image linked by URL
To process the image linked by URL, we can simply covert the URL to base 64 code and to do the same process as above.
First, make sure the input is a URL or base 64 code, becuase sometimes we copy the address of an image on the Internet, what we copied is acturally not a URL but base 64 code. If it is a URL, covert to base 64 code, if it is base 64 code, send to API directly.
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/URL.png)

### Details
processing effect:
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/processing.png)
This is acturally two masks, the first one is to make the orignial image darker, and the second one is an icon representing processing. hidden both originally, when users make some operation, visualise both and when the server send back the response, hidden both.
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/mask.png)

error notes:
When there are something wrong, get the error status returned by the server and display corresponding notes.
![image](https://github.com/jiaxiuli/Face-Recognition-and-Processing/blob/master/image/notes.png)
