APPROACH:

I found this task more approachable to attempt after beginning task 1. I read through the Dragonfly Documentation (paying special attention to the
sections indicated in the pdf). This combined with researching I had done for task 1 gave me a vague idea of my process.



SETUP:

I began by installing Oracle VirtualBox and setting up Ubuntu as I primarily operate off of a windows device.
I had not had to do this prior as I had it set up on my Macbook that was stolen some months back, but now it was necessary.
An IMPORTANT note here is to make sure that the Ubuntu Virtual Machine being setup has AMPLE space when beginning as this process
easily filled up ~15 GB before I even knew what was happening and led to me having to take a break to diagnose and troubleshoot.
This was primarily due to me attempting to use the docker process outlined in the repo, which I would not recommend as it felt like
I had less control (and certainly less space before pruning my active container).


All this to say due to the libraries and data being downloaded I would allocate 20-30 GB to your machine, this may be genrous but
you don't want your process to be halted due to insufficient disk space.


I then cloned the repo on my virutal machine and followed the process outlined by the Readme.md in the Dragonfly repo, please note that any unsuccesful downloading of prerequistes will prevent you from continuing so you will want ample disk storage on Ubuntu.



DOWNLOAD PREREQUISITES:


-apt-get update  && apt-get install build-essential software-properties-common -y  && add-apt-repository ppa:ubuntu-toolchain-r/test && apt-get update  && apt-get install gcc-9 g++-9 -y  && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 60 --slave /usr/bin/g++ g++ /usr/bin/g++-9


-add-apt-repository ppa:jonathonf/ffmpeg-4


-apt-get install -y  ffmpeg  libgflags-dev libgoogle-glog-dev libboost-all-dev libavcodec-dev libavformat-dev libswscale-dev libdouble-conversion-dev libfmt-dev libevent-dev libssl-dev cmake  mahimahi


*FOR FOLLY AND FMT*


If you are running from an Ubuntu virtual machine you will have to edit the makefile outlined before executing the final command: make install
for both folly and fmt.
This is because the default has it create a directory in a path that does not exist on a UBUNTU machine ( 'usr/local/...').
In the files titled "cmake_install.cmake" located in 'home/[YOURUSER]/Dragonfly/third-party-lib/[folly or fmt respectively]/build' you will need
to open the file and under the first block titled "# Set the install prefix", you should see a string for a path discussed earlier that
you will alter to one of your choice. From there you can proceed with the "make install" command


FMT:

-cd ~/Dragonfly/third-party-lib/fmt && mkdir build && cd build && cmake .. && make -j2 && make install


Folly:

-cd ~/Dragonfly/third-party-lib/folly-2021.03.15.00 && mkdir _build && cd _build && cmake .. && make -j2 && make install


And now after navigating back to the Dragonfly directory we can now finally build:

-cd system && mkdir build && make -f Makefile_ubuntu


We have now made our build but we must prepare some things before runtime such as segmenting our desired video. We navigate to the videos_preperation directory located in the Dragonfly directory. We then need to follow along with the readme, importantly I found there
were some packages I was missing (even after downloading the prerequisites listed) so pay attention to any errors that pop up. Make sure any packages downloaded to compensate are in the python3 environment (by using pip3 rathr then pip for commands).

For me I additionally needed the following commands:

-pip3 install numpy

Also when installing the VQMT prerequisite, which requires the openCV prerequisite the link was broken so I had to do some exploration on my own.
To successfully install I needed to execute the following:

-pip3 install --upgrade pip
-pip3 install opencv-python
