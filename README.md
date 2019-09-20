3rd-Year-IOT-project on Eye Detection and Recognition System

----	Introduction

 Face and Eye detection is one of the fundamental applications used in face recognition technology.
 Facebook, Amazon, Google and other tech companies have different implementations of it.
 Before they can recognize a face or eye, their software must be able to detect it first.
 Amazon has developed a system of real time face/eye detection and recognition using cameras.
 Facebook uses it mostly on photos that their users upload in order to suggest tagging friends.


 ----	Requirements
 Any operating system that will support OpenCV and Python (Windows, Linux, MacOS)
 Python
 OpenCV-Python
 Haar Cascades Data File
 i3 or higher core processor (CPU)/ 2.1 GHz or higher
 Photo images for testing



--- Dependencies & steps

Change directory to server's root, or wherever you want to place your workspace

cd ~

sudo apt-get update

sudo apt-get upgrade

First, let's make ourselves a nice workspace directory:

mkdir opencv_workspace

cd opencv_workspace

Now that we're in here, let's grab OpenCV:

sudo apt-get install git

git clone https://github.com/Itseez/opencv.git

We've cloned the latest version of OpenCV here. Now let's get some essentials:

Compiler: sudo apt-get install build-essential

Libraries: sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev

Python bindings and such: sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev



Finally, let's grab the OpenCV development library:

sudo apt-get install libopencv-dev


----	What is  "Eye Detection" or “Face Detection” ?

Eye detection is a type of application classified under “computer vision” technology.
It is the process in which algorithms are developed and trained to properly locate eyes/faces or objects (in object detection, a related system), in images.
 These can be in real time from a video camera or from photographs.
 An example where this technology is used are in airport security systems.
 In order to recognize an eye/face, the camera software must first detect it and identify the features before making an identification.
 Likewise, when Facebook makes tagging suggestions to identify people in photos it must first locate the face and then eyes.
 On social media apps like Snapchat,
 Eye/face detection is required to augment reality which allows users to virtually wear dog face masks using fancy filters.
 Another use of eye detection is in smartphone face ID security.
In this project, We implemented a system for locating faces and eyes in digital images. These are in JPEG format only.


Before we continue, we must differentiate between face recognition and face detection.
They are not the same, but one depends on the other.
In this case face recognition needs face detection for making an identification to “recognize” a face.

Face detection uses classifiers, which are algorithms that detects what is either a face(1) or not a face(0) in an image.
Classifiers have been trained to detect faces using thousands to millions of images in order to get more accuracy.
OpenCV uses two types of classifiers, LBP (Local Binary Pattern) and Haar Cascades.

We will be using the Haar classifier.


----	What is Haar Cascade??

A Haar Cascade is based on “Haar Wavelets” which Wikipedia defines as:
A sequence of rescaled “square-shaped” functions which together form a wavelet family or basis.
It is based on the Haar Wavelet technique to analyze pixels in the image into squares by function.
This uses machine learning techniques to get a high degree of accuracy from what is called “training data”.
This uses “integral image” concepts to compute the “features” detected.
Haar Cascades use the Adaboost learning algorithm which selects a small number of important features
from a large set to give an efficient result of classifiers.

---- Training data is in the file

1) The training data used in this project is an XML file called:
haarcascade_frontalface_default.xml


2)haarcascade_eye.xml

----	Algorithm

So when you want to build a Haar Cascade, you need "positive" images, and "negative" images.
The "positive" images are images that contain the object you want to find. This can either be images that just mainly have the object,
or it can be images that contain the object, and you specify the ROI (region of interest) where the object is. With these positives,
 we build a vector file that is basically all of these positives put together.
 One nice thing about the positives is that you can actually just have one image of the object you wish to detect,
 and then have a few thousand negative images. Yes, a few thousand. The negative images can be anything,
  except they cannot contain your object.

From here, with your single positive image, you can use the opencv_createsamples command to actually create a bunch of positive examples,
 using your negative images. Your positive image will be superimposed on these negatives, and it will be angled and all sorts of things.
 It actually can work pretty well, especially if you are really just looking for one specific object.
 If you are looking to identify all screwdrivers, however, you will want to have thousands of unique images of screwdrivers, rather than using the opencv_createsamples to generate samples for you.
 Here we will keep it simple and just use one positive image, and then create a bunch of samples with our negatives.


----	How do we actually implement this process?

Steps:

1.Collect "Negative" or "background" images.
--make sure your object will not present on them
2.Collect or create "positive" images.
--thousands of images of the object.
3. Create a positive vector file by stitching together all positive neg_images_link
-- done with open cv commands
4.Train Cascade
--done with opencv cmd


----	Understanding the code
Simple enough, this script will visit the links, grab the URLs, and proceed to visit them. From here,
we grab the image, convert to grayscale, resize it, then save it. We use a simple counter for naming the images.
Go ahead and run it. As you can probably see, there are a lot of missing pictures and such. That's okay. More problematic is
some of these error pictures.
Basically all white with some text that says they are no longer available,
 rather than serving and HTTP error. Now, we have a couple choices.
  We can just ignore this, or fix it. Hey, it's an image without a watch, so whatever right?
  Sure, you could take that opinion, but if you use this pulling method for positive then this is definitely a problem.
  You could manually delete them... or we can just use our new Image Analysis knowledge to detect these silly images and remove them!



We are going to use the detectMultiscale module from OpenCV.
 What this does is create a rectangle with coordinates (x,y,w,h) around the face and eyes detected in the image.
This contains code parameters that are the most important to consider.

scaleFactor: The value indicates how much the image size is reduced at each image scale.
A lower value uses a smaller step for downscaling. This allows the algorithm to detect the face.
It has a value of x.y, where x and y are arbitrary values you can set.

minNeighbors: This parameter specifies how many “neighbors” each candidate rectangle should have.

A higher value results in less detections but it detects higher quality in an image. You can use a value of X that specifies a finite number.
minSize: The minimum object size.
By default it is (30,30). The smaller the face in the image, it is best to adjust the minSize value lower.

----	For recognising the images:

 The code can detect faces, but it would still require verification from the user.
 This is therefore a fully intelligent system and  it requires interaction from the user.

----	




