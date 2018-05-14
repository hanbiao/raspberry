***Edge Detection***

Edge detection algorithm based on the Sobel operator ：This algorithm works by calculating the **gradient of the intensity of the image at each point**, finding the direction of the change from light to dark and the magnitude of the change. This magnitude corresponds to how sharp the edge is. 



To calculate the gradient of each point in the image, the image is convolved with the Sobel Kernel. **Convolution is done by moving the kernel across the image, one pixel at a time. At each pixel, the pixel and its neighbours are weighted by the corresponding value in the kernel, and summed to produce a new value**. This operation is shown in the following diagram.

```
~~~~~~~~~~~~~~~~~~~            ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
| k00 | k10 | k20 |            | i00 | i10 | i20 | i30 | ..
|~~~~~+~~~~~+~~~~~+            |~~~~~+~~~~~+~~~~~+~~~~~+~~~
| k01 | k11 | k21 |            | i01 | i11 | i21 | i31 | ..
|~~~~~+~~~~~+~~~~~+            |~~~~~+~~~~~+~~~~~+~~~~~+~~~
| k02 | k12 | k22 |            | i02 | i12 | i22 | i32 | ..
|~~~~~+~~~~~+~~~~~+            |~~~~~+~~~~~+~~~~~+~~~~~+~~~
                               | i03 | i13 | i23 | i33 | ..
Applying the kernel to the     |~~~~~+~~~~~+~~~~~+~~~~~+~~~
to the first pixel gives us    |  .. |  .. |  .. |  .. | ..	
an output value for that
pixel

     o00 = k11 * i00 + k12 * i01 + k21 * i10 + k22 * i11
```

Edge detection using the **Sobel Operator applies two separate kernels to calculate the x and y gradients in the image. **The length of this gradient is then calculated and normalised to produce a single intensity approximately equal to the sharpness of the edge at that position.

The kernels used for Sobel Edge Detection are shown below.

```
~~~~~~~~~~~~~
|-1 | 0 | 1 |
|~~~+~~~+~~~|
|-2 | 0 | 2 |
|~~~+~~~+~~~|
|-1 | 0 | 1 |
~~~~~~~~~~~~~
x gradient kernel

~~~~~~~~~~~~~
|-1 |-2 |-1 |
|~~~+~~~+~~~|
| 0 | 0 | 0 |
|~~~+~~~+~~~|
| 1 | 2 | 1 |
~~~~~~~~~~~~~
y gradient kernel
```

## 2 The Algorithm

Now the algorithm can be broken down into its constituent steps

```
1 Iterate over every pixel in the image
2 Apply the x gradient kernel
3 Apply the y gradient kernel
4 Find the length of the gradient using pythagoras' theorem //毕达哥拉斯理论-勾股定理..
5 Normalise the gradient length to the range 0-255
6 Set the pixels to the new values
```

## 3 Extended

With the lib, we can implement some other image processing algorithms. The algorithm we will look at is this tutorial is a fairly basic one. The aim is apply a Colour Key to an image, picking out a specific colour or range of colours in the image and removing them, or replace them with a seperate background image. //背景颜色替换

[Page link](http://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/image-processing/colour_key.html)

