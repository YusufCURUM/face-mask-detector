# face-mask-detector  

Face masks are crucial in minimizing the propagation of Covid-19, and are highly recommended or even obligatory in many situations. In this project, i develop a pipeline to detect unmasked faces in images. This can, for example, be used to alert people that do not wear a mask when entering a building.  

### My pipeline consists of three steps:  
- Detect all human faces in an image  
- Make a mask/no_mask prediction for each of them  
- Return an annotated image with the predictions


### Technologies
- Python 3.7
- Tensorflow2 / Keras

### Data collection
Our training data is based on the VGGFace2 dataset. This dataset provides a collection of faces that are captured in the wild with different ethnicities, ages and emotions. I use 4941 images of this dataset, and apply an artificial masks to half of them. This data will be used to train our mask/no_mask classifier.  
My validation and testing data consists of images of people with and without masks that i collected from various sources that provide images with permissive licences (e.g. pexels.com, unsplash.com). I have manually annotated all faces in the collected images, and labeled them as being masked or not (using the makesense.ai annotation tool). I collected 273 images which contain 524 faces (246 masked and 278 non-masked). The images are split 50/50 over the validation set and test set.   

### Data preprocessing
Labeled data of masked faces is hard to come by, which is why i decided to set the overall still limited set of real masked faces that i have collected apart for validation and testing. Artificially generated masks that are used for training are generated as follows:  

1. Detect the face in the image
2. Find the face landmarks, more specifically we need the location of the nose and chin
3. Apply an image of a mask to the face with the position based on the face landmarks

