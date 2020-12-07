# Character-Sequence-Recognition

The work is based on Matthew Earl's [repository](https://github.com/matthewearl/deep-anpr).

### Improvement
Recognition of character from street view images with different real life environments. It covers learning more comprehensively from the images that comes from natural lighting scene, different weather conditions, at varied time.

## Data Augmentation

* How it now became very hard identification problem: 
	* Orientation
	* Font family
	* Different Pixel color of plate and that of whole image

We have more than **100,000 images** of around 36 GB 
We break data into 10,000 images batches for training

Consisting round *48 classes* of different locations

Also, our model is not only trained over GRAYSCALED images, 
but includes synthesised images those are colored & gray as well for prediction on real images.

## Resnet Model

**CNN_1 Phase 1** | **CNN_2 Phase 2** | **Fully Connected layer**
------------|------------|-----------
*Step 1*      | *Detection* | *Decision*
 | | 
48 filter (128x64) In each, we find  **Pr[how_much_plate_is_in_the_frame]** by separating pixel by color | Move the stride over the layers to give the output a window coordinate, from which we can tell if a plate is in that stride as a whole | We use Relu function (like one hot encoding) to give the sequence from the Probability our model calculate
| |
*Step 2* 
| |
Find **Pr[the_character_in_the_plate_is_some_character_from_the_label]**

## Result

<img src="https://github.com/shashankdahiya/Character-Sequence-Recognition-/blob/master/Training_Accuracy.png" width="250"> | <img src="https://github.com/shashankdahiya/Character-Sequence-Recognition-/blob/master/out_4_1.jpg" width="250">
-----|------
## Installation
Use below mentioned git commands to clone the repo:
```
git init
git clone https://github.com/sdahi002/Character_Sequence_Recognition/
```

Now from the same directory where repo has been cloned, in the same order, run following python scripts:
> Python 3.7+ 

To extract and set train and test data, run these commands (you can set your own data as well, just change train input data file command to point to your data file):
`./extractbgs.py SUN397.tar.gz`
`./gen.py 1000`

Setup the model, and train the model. Training model can take around 4 to 6 hours, but if you train it more than that time, then it will improve the model's performance until some extent (do not train for more than 12 hours, it can overfit the model):
```
python model.py
python train.py
python detect.py in.jpg weights.npz out.jpg
```
> in and out are the image that you want to predict the sequence and show the results.

-----|-----------|-----------|-----------|-----------|-----------|-----------|-----------|------
