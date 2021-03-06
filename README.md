# ScanGameBackend
This is the FastAPI backend that supports my ScanGame Apps. It can detect certain objects from pictures. This API serves my iOS/Android apps for the game here: https://github.com/two-trick-pony-NL/PhotoScavenger

API documentation here:  
- https://scangame.herokuapp.com/docs

Here is a in-game screenshot: <br>
![ezgif com-gif-maker](https://user-images.githubusercontent.com/71013416/178448499-3f547173-43ab-41b2-967a-a1f9ae8dd9a0.gif)

# Demo on Heroku: 
[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/521a10c88390c265b54d?action=collection%2Fimport)
- URL: https://scangame.herokuapp.com
- New assignment a random object to scan and it's emoji: https://scangame.herokuapp.com/newassignment/2001
* In the new assignment call you need to add a number of points, more points means a more difficult next object

- Example (returns JSON without receiving a picture: https://scangame.herokuapp.com/exampleresponse
- Endpoint for POST requests: http://scangame.herokuapp.com/uploadfile/boat
*Replace boat with any of these objects to detect them: 
```
background", "earoplane", "bicycle", "bird", "boat", "bottle", "bus", "car", "cat", "chair", "cow", "diningtable", "dog", "horse", "motorbike", "person", "pottedplant", "sheep", "sofa", "train", "tvmonitor
```

# What does it do:
This backend can check images to see if a certain object is on the picture. For instance: you can check if there is a cat on a particular photo. The backend will then return a false or true for that object depending on whether it was found. It will also return a list objects it managed to find. This allows you validate in case of false negatives, to see what the model thought was on the picture. See an example below. 

# How does it work: 
you make a POST request with a image in the formdata (content type 'file'). 
For instance this image: 

![Schermafbeelding 2022-06-18 om 11 26 33](https://user-images.githubusercontent.com/71013416/175918302-bd99786a-9d4f-49d7-a90c-9bbbff847035.png)

and it returns an image with the detected objects:
![scanned_imagee0dee0c1-3512-4617-8a3d-4d19b80c85e7](https://user-images.githubusercontent.com/71013416/177133306-d0eab947-6013-4925-94ce-dccb3106af1a.jpg)

# How to run: 

Simply clone the repo and run: 
```
gh repo clone two-trick-pony-NL/ScanGameBackend && cd ScanGameBackend
```
 
```
uvicorn main:app --host 0.0.0.0 --port 80 --reload
```

# Request / Response -- Local

Call
```
http://localhost:80/uploadfile/bicycle
```

or 
```
http://localhost:80/uploadfile/person
```

Response (for bicycle)
```
{
    "Searchedfor:": "boat",
    "Wasfound": false,
    "OtherObjectsDetected": [
        "person",
        "person",
        "person",
        "person",
        "bicycle",
        "motorbike",
        "bicycle",
        "motorbike",
        "bicycle"
    ],
    "Processed_FileName": "scanned_image54e46fb8-93f8-43ad-a8ec-99eb83f260af.jpg",
    "file_url": "image54e46fb8-93f8-43ad-a8ec-99eb83f260af.jpg",
    "listofobjectsWithConfidence": [
        {
            "person": 100
        },
        {
            "person": 100
        },
        {
            "person": 100
        },
        {
            "person": 100
        },
        {
            "bicycle": 97
        },
        {
            "motorbike": 91
        },
        {
            "bicycle": 75
        },
        {
            "motorbike": 48
        },
        {
            "bicycle": 28
        }
    ]
}
```
Supported objects
```
["background", "earoplane", "bicycle", "bird", "boat", "bottle", "bus", "car", "cat", "chair", "cow", "diningtable", "dog", "horse", "motorbike", "person", "pottedplant", "sheep", "sofa", "train", "tvmonitor"]
```

Getting a new assignment
```
http://localhost:8000/newassignment
```

response:
```
{"dog":"????"}
```
# Postman example: 

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/521a10c88390c265b54d?action=collection%2Fimport)

![Schermafbeelding 2022-07-04 om 12 14 33](https://user-images.githubusercontent.com/71013416/177134451-899276f5-a8e2-4127-b358-2c4ae46e4cee.png)


# Acknowledgement: 
- I took most of the Image detection from the tutorial by NeuralNine: https://www.youtube.com/watch?v=lE9eZ-FGwoE&t=2s 
