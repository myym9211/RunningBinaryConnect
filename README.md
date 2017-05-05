# Title : Windows 10 Guide to run BinaryNet
# Author : Yameen Malik
# Timestamp: 27/3/2017 02:00 AM
#################################################################################################
# This guide will get you through how to run the code for the paper titled						#
# BinaryNet: Training Deep Neural Networks with Weights and Activations Constrained to +1 or -1 #
# avaialable at : https://arxiv.org/pdf/1602.02830.pdf?											#
# git repository at : https://github.com/MatthieuCourbariaux/BinaryNet							#
#################################################################################################

-------------------
1. Install Anaconda
-------------------
	1a. Goto https://www.continuum.io/downloads and download Anaconda 2.7 for 64 bit operating system.
	2a. Once download run .exe file and follow the guidelines and keep everything to default.

-----------------
2. Install Theano
-----------------
	Firstly open CMD from start menu and perform following steps.
	2a. Update conda type:	conda update conda
	2b. Update all pacakages type : conda update --all
	2c. Install Theano's pre-requisite type: conda install mingw libpython
	2d. Then install theano type : pip install theano

-----------------------------------------
3. Update Theano to Bleeding Edge version
-----------------------------------------
	3a. Install git command using : conda install git
	3b. Install Bleeding edge by : pip install --upgrade --no-deps git+https://github.com/Theano/Theano.git
	3c. Just for precaution update conda again : conda update conda

-------------------
4. Install Pylearn2
-------------------
	4a. From cmd type conda install Pylearn2
	4b. Goto start menu and search for Edit Enviroment variables open it and select Environment Variables.
		-> Over here under User variables and system variables create a variable named PYLEARN2_DATA_PATH 
		   and set its path to the directory where you will be keeping your training data for mnist,cifar,svhn.
		   In my case it is C:\Users\Malik\Desktop\BC\data
		-> Remember this Path as it would be used while running the code in step 10.
------------------
5. Install Lasagne
------------------
	5a. Install lagane by using conda install lasagne
	5b. Upgrade lasagne to latest by typing : pip install --upgrade https://github.com/Lasagne/Lasagne/archive/master.zip

-----------------------------
6. Install Visual Studio 2015
-----------------------------
	6a. Download VS2015 using google and extract it.
	6b. Run installation file and when prompted with CUSTOM or EXPRESS installation select CUSTOM.
		-> In custom installation select ALL THE PROGRAMMING languages box and then continue.
		-> Else you will be beating your head against the wall like me !!  
		
--------------------------------
7. Setting up the GPU for Theano
--------------------------------
	Make sure that you have a cuda enabled graphics card. See the list https://developer.nvidia.com/cuda-gpus
	And also make sure that you have the latest driver installed for the graphics card. If not then run
	to NVDIA site to download the latest one come back and follow these steps.
	
	7a. Download the appropriate CUDA driver for the graphics card from here https://developer.nvidia.com/cuda-downloads
		-> Select Windows
		-> Select 10
		-> Select exe local
		-> Kill the download button
	7b. Once the downloaded open installation file and select CUSTOM installation.
		-> Check only the CUDA box and uncheck all other boxes.
		-> If the nvdia shows installation error then you either dont have the latest driver for the graphics card
		   or you havent installed Visual Studio 2015 correctly.
	7c. If all ok, then open cmd and to test that cuda is up and running type nvcc - V. If it shows your GPU then good
		else find out where you messed up!

-----------------------
8. Link GPU with Theano
-----------------------
	8a. Goto the root directory where you installed Anaconda environment. While installing Anaconda, if you kept everything
	    to default then it will be in "C:\Users\YourUserName\". Here you will find the Anaconda2. If not here then search it.
	8b. Once at the root, create a new file with the name ".theanorc", open it and put the following content in it.
	-------------------------------------------------------------------------------------------------------------------
		[global]
		floatX = float32
		device = gpu
		mode=FAST_RUN

		[cuda]
		root = C:\Program Files\NVIDIA Corporation\Installer2\CUDAToolkit_8.0.{03A68DD2-B457-4C3B-9B1E-1FB837E6C727}


		[nvcc]
		flags = -LC:\Users\Malik\Anaconda2\libs
		compiler_bindir = E:\Installed Softwares\VisualStudio2015\VC\bin
		fastmath = True
	-------------------------------------------------------------------------------------------------------------------
	8c. Set the path of following variables:
		-> root : Assign it the path of directory where CUDA is. 
		-> flags : Assign it the path of libs folder in Anaconda directory.
		-> compiler_bindir: Assign it the path of the folder consisting cl.exe, it is in VC folder inside Visual Studio
		
--------------
9. TEST THEANO
--------------
	9a. Open cmd and type python
	9b. type import theano and hit enter
	9c. If it shows any error, then you messed up else every thing is fine. It will probably show a warning.

------------------
10. Running CODES
------------------
	10a. Download the git repository from https://github.com/MatthieuCourbariaux/BinaryConnect and extract it.
	10b. This directory contains python scripts for mnist, cifar10 and svhn, so this is how you run it.
	=====
	MNIST
	=====
		-> To run mnist.py first download the datasets and labels from http://yann.lecun.com/exdb/mnist/
		-> Once downloaded extract them and you will have 4 files with the names
			1) train-images.idx3-ubyte
			2) train-labels.idx1-ubyte
			3) t10k-images.idx3-ubyte
			4) t10k-labels.idx1-ubyte
		-> Replace the dot '.' from the names and replace them with '-' hyphens so that their names are such
			1) train-images-idx3-ubyte
			2) train-labels-idx1-ubyte
			3) t10k-images-idx3-ubyte
			4) t10k-labels-idx1-ubyte
		-> Now remember the path from step 4?? Now goto that path in my case it was C:\Users\Malik\Desktop\BC\data
		   create a folder named mnist in this directory and add all 4 files in this mnist folder.
		-> Now open cmd and type python mnist.py to start training your model.
		
		
=======================================================================
[global]
floatX = float32
device = gpu
optimizer = fast_run


[cuda]
root = C:\Program Files\NVIDIA Corporation\Installer2\CUDAToolkit_8.0.{811D59BF-D242-46E3-8A87-F501384E5613}

[lib]
cnmem = 0.8

[nvcc]
flags = -LC:\Users\Malik\Anaconda2\libs
compiler_bindir = E:\Installed Softwares\VC\bin
fastmath = True

[blas]
ldflags = -llapack -lblas

