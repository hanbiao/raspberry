# How to install OpenCV 3 #

[Page Link](https://www.pyimagesearch.com/2016/04/18/install-guide-raspberry-pi-3-raspbian-jessie-opencv-3/)

### Step #0: Expand filesystem

The first thing you should do is expand your filesystem to include *all available space* on your micro-SD card 

```
sudo raspi-config
#Expand File System
sudo reboot
```

You can verify that the disk has been expanded by executing df -h  and examining the output, OpenCV, along with all its dependencies, will need a few gigabytes during the compile, so you should delete the Wolfram engine to free up some space on your Pi: 

```
sudo apt-get purge wolfram-engine
```

### Step #1: Install dependencies

The first thing we should do is update and upgrade any existing packages, followed by updating the Raspberry Pi firmware.

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo rpi-update
```

You’ll need to reboot your Raspberry Pi after the firmware update: 

```
$ sudo reboot
```

Now we need to install a few developer tools:

```
sudo apt-get install build-essential git cmake pkg-config
```

Now we can move on to installing image I/O packages which allow us to load image file formats such as JPEG, PNG, TIFF, etc.

```
$ sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
```

We also need video I/O packages. These packages allow us to load various video file formats as well as work with video streams 

```
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
$ sudo apt-get install libxvidcore-dev libx264-dev
```

We need to install the GTK development library so we can compile the highgui  sub-module of OpenCV, which allows us to display images to our screen and build simple GUI interfaces 

```
$ sudo apt-get install libgtk2.0-dev
```

Various operations inside of OpenCV (such as matrix operations) can be optimized using added dependencies 

```
$ sudo apt-get install libatlas-base-dev gfortran
```

Lastly, we’ll need to install the Python 2.7 and Python 3 header files so we can compile our OpenCV + Python bindings 

```
$ sudo apt-get install python2.7-dev python3-dev
```

### Step #2: Grab the OpenCV source code

Grab the 3.4.1  version of OpenCV from the [OpenCV repository](https://github.com/Itseez/opencv) 

```
$ cd ~
$ wget -O opencv.zip https://github.com/Itseez/opencv/archive/3.1.0.zip
$ unzip opencv.zip
$ wget -O opencv_contrib.zip https://github.com/Itseez/opencv_contrib/archive/3.1.0.zip
$ unzip opencv_contrib.zip
```

### Step #4: Python 2.7 or Python 3?

Before we can start compiling OpenCV on our Raspberry Pi 3, we first need to install pip , a Python package manager: 

```
$ wget https://bootstrap.pypa.io/get-pip.py
$ sudo python get-pip.py
```

**Virtual environment** is a *special tool* used to keep the dependencies required by different projects in separate places by creating *isolated, independent* Python environments for each of them. It also keeps your global site-packages  neat, tidy, and free from clutter. 

It’s **\*standard practice*** in the Python community to be using virtual environments of some sort, so I *highly recommend* that you do the same 

```
$ sudo pip install virtualenv virtualenvwrapper
$ sudo rm -rf ~/.cache/pip
```

Now that both virtualenv  and virtualenvwrapper  have been installed, we need to update our ~/.profile  file 

```
# virtualenv and virtualenvwrapper
export WORKON_HOME=$HOME/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh
```

Now that we have our ~/.profile  updated, we need to reload it to make sure the changes take affect. You can force a reload of your ~/.profile  file by:

1. Logging out and then logging back in.

2. Closing a terminal instance and opening up a new one

3. Or my personal favorite, **\*just use the source  command:***

   ```
   $ source ~/.profile
   ```

#### Creating your Python virtual environment

Next, let’s create the Python virtual environment that we’ll use for computer vision development ,This command will create a new Python virtual environment named cv  using **\*Python 3.4*** 

```
 mkvirtualenv cv -p python3
```

The cv  Python virtual environment is **\*entirely independent and sequestered*** from the default Python version included in the download of Raspbian Jessie. Any Python packages in the *global* site-packages  directory *will not* be available to the cv  virtual environmen 

#### How to check if you’re in the “cv” virtual environment

If you ever reboot your Raspberry Pi; log out and log back in; or open up a new terminal, you’ll need to **use the workon  command to re-access the cv  virtual environment; ** the mkvirtualenv  command — **\*this is entirely unneeded!*** The mkvirtualenv  command is meant to be executed only once: to actually *create* the virtual environment. 

```
$ source ~/.profile   // to set up shell config
$ workon cv
```

*if you see the text (cv)  preceding your prompt, then you \**are** in the cv  virtual environment:* 

### Installing NumPy on your Raspberry Pi

you should now be in the cv  virtual environment (which you should stay in for the rest of this tutorial). Our only Python dependency is [NumPy](http://www.numpy.org/), a Python package used for numerical processing: 

```
$ pip install numpy
```

### Step #4: Compile and Install OpenCV

Double-check that you are in the cv  virtual environment by examining your prompt (you should see the (cv)  text preceding it ; then, we can setup our build using CMake 

```
$ cd ~/opencv-3.1.0/
$ mkdir build
$ cd build
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-3.1.0/modules \
    -D BUILD_EXAMPLES=ON ..
```

Finally, we are now ready to compile and install OpenCV 

```
$ make
... 1hour
$ sudo make install
$ sudo ldconfig

```

### Step #6: Finish installing OpenCV on your Pi

OpenCV + Python bindings should be installed in/usr/local/lib/python3.4/site-packages 

After renaming to cv2.so , we can sym-link our OpenCV bindings into the cv virtual environment for Python 3.5 

```
$ cd /usr/local/lib/python3.5/site-packages/
$ sudo mv cv2.cpython-35m.so cv2.so

$ cd ~/.virtualenvs/cv/lib/python3.5/site-packages/
$ ln -s /usr/local/lib/python3.5/site-packages/cv2.so cv2.so
```

### Step #7: Testing your OpenCV 3 install

Open up a new terminal, execute the source  and workon  commands, and then finally attempt to import the Python + OpenCV bindings 

```
$ source ~/.profile 
$ workon cv
$ python
>>> import cv2
>>> cv2.__version__
...
```

