
# Face Recognizer

Real time face recognition model from scratch by detecting the faces, draw bounding box around them and recognize the face by comparing the input image with some verification images that the model has for each person.

The model consists of two parts:

1- Face tracker to detect the face and draw bounding box around it.

2- Siamese model to recognize the person.

## Face Tracker model:

Worked on it before , you can find all details in this repo:

https://github.com/Mustafa-Osama/Face_Tracker

## Siamese model:

### Defenition

A Siamese neural network (sometimes called a twin neural network) is an artificial neural network that uses the same weights while working in tandem on two different input vectors to compute comparable output vectors.

Uses of similarity measures where a twin network might be used are such things as recognizing handwritten checks, automatic detection of faces in camera images, and matching queries with indexed documents. The perhaps most well-known application of twin networks are face recognition, where known images of people are precomputed and compared to an image from a turnstile or similar. It is not obvious at first, but there are two slightly different problems. One is recognizing a person among a large number of other persons, that is the facial recognition problem. DeepFace is an example of such a system.In its most extreme form this is recognizing a single person at a train station or airport. The other is face verification, that is to verify whether the photo in a pass is the same as the person claiming he or she is the same person. The twin network might be the same, but the implementation can be quite different.

### Dataset

In this project, the model will be designed to recognize 5 faces so I have collected images for 5 persons using web cam.

I have captured about 80 images for each person but this number of images will be increased using augmentation.

I have created a folder for each person, each folder of these 5 folders has 3 subfolders (ancher, positive, negative)

- Ancher and positive folders have images for the right person.
- Negative folder has images for the other 4 persons.

### Augmentation

As I have only 80 images (40 --> ancher, 40 -->positive) for each person so we need augmentation to increase the number of images.

After augmentation, each folder of ancher, positive and negative will has 1200 images instead of 40 images.

### Model

The model consists of a sequence of convolutional layers, each of which uses a single channel with filters of varying size and a fixed stride of 1. The number of convolutional filters is specified as a multiple of 16 to optimize performance. The network applies a ReLU activation function to the output feature maps.

![siamese](https://user-images.githubusercontent.com/113447865/193626621-acd17d34-e584-4523-9474-7c805663a69a.png)

The units in the final convolutional layer are flattened into a single vector. This convolutional layer is followed by a fully-connected layer, and then one more layer computing the induced distance metric between each siamese twin, which is given to a single sigmoidal output unit.


## FaceRecognition model

The is only cobination between FaceTracker model and Siamese model.

The pipeline of process:

- Capturing image.
- Pass the image as an input to FaceTracker model to detect if there is a face in the image or not.
- If there is a face in the image, the image will be passed into Siamese model to recognize the person.
- FaceTracker model will draw bounding box around the face and take the output of Siamese network as the person's name to put it as a text for the box.
