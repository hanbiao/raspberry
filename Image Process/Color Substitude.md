## Extended Application

With the lib, we can implement some other image processing algorithms. The algorithm we will look at is this tutorial is a fairly basic one. The aim is apply a Colour Key to an image, picking out a specific colour or range of colours in the image and removing them, or replace them with a seperate background image. //背景颜色替换

[Page link](http://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/image-processing/colour_key.html)

## The Algorithm

The algorithm we will use takes in a reference colour and a threshold. The threshold dictates how far away from the reference colour a pixel's colour can be and still pass.

To calculate which pixels pass, the difference between the 2 pixels colour channels is compared and the distance between them is calculated using the Pythagorean formula. The algorithm is outlined in pseudo-code below.

```
For each pixel:
1 Get the red green and blue values of the pixel
2 Subtract the red, green and blue values of the pixel from the respective
	channels of the comparison colour.  This is the colour difference in each
	colour axis.
3 Calculate the length of the line represented by the colour difference
	length = sqrt( sqr(red difference) + sqr(green difference) + sqr(blue difference) )
4 Compare this length to the threshold.  If it passes, mark it white, otherwise
	mark it black
```