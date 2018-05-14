***Image Pi – Basic image processing***

[Page link](http://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/image-processing/)

1. **Image**

   > Within a Computer, images are stored as a two dimensional array of pixels (**pic**ture **el**ement). The array can be thought of as a long table of row and columns, where each entry corresponds to a single pixel and each pixel stores the colour of the image at that single point. To understand how each colour is stored we will look at colour spaces. 

2. **Colour Space**

   > The value stored for each pixel in the image depends on the ***colour space*** and ***colour model*** being used.  The colour model describes how colours are represented by a set of numbers, where each number corresponds to a different colour 'channel'. The colour space is the mapping of the channels of the colour model to absolute reference values.  For example the widely used colour space sRGB is based on an RGB colour model, where each pixel has values in the Red, Green and Blue colour channels. Each value represents the intensity of that colour relative to the absolute reference colours defined by the sRGB colour space. 

   > There are a whole range of colour models and spaces, another widely used colour model is CMYK, standing for Cyan, Magenta, Yellow and Key (Black). This colour model is used in printing and differs from the RGB colour model as it is a subtractive colour model rather than an additive model; So in the RGB colour model, a combination of full intensities in Red, Green and Blue corresponds to white, whereas in CYMK it corresponds to black.

   > When the colour of a pixel is stored, it is stored as a tuple (ordered list) of values, with values for each channel defined by the colour model. The range each value takes is defined by the colour depth of the image, which is the number of bits used to store the colour of a single pixel. For an image based on the RGB model with a colour depth of 24 bits per pixel, 8 bits are used for each of the 3 channels giving a range of 0 to 255 (inclusive). This decimal value would then be stored internally as its binary equivalent. Sometimes the number of bits per pixel is defined in terms of the number of bits used per colour channel. So a pixel format named RGB565 would use 5 bits for the red and blue channels, and 6 bits for the green.



***download libarary and install***

```
sudo wget http://www.cl.cam.ac.uk/downloads/freshers/image_processing.tar.gz
sudo tar -xf image_processing.tar.gz
cd xx/library
sudo make install

log:
chmod 755 libimgproc.so
chmod 755 imgproc.py
chmod 755 imgproc.h
cp libimgproc.so /usr/lib/
cp imgproc.h /usr/include/
cp imgproc.py /usr/local/lib/python2.7/dist-packages/
sudo apt-get install libsdl1.2debian
```

> The `library` directory contains the library, python module and C header file. It also contains the install script to place these files into the correct place in the filesystem.
>
> `examples` contains the code from the examples in these tutorials.
>
> `source` contains the source code for the library and python module, you can look here if you're interested in how the library works. If you want to alter and build the source, you can look at `Makefile` to see the build steps.



- 测试程序

  运行example文件夹下的python脚本可以进行测试