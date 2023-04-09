# Installation Script for LLaMa 7B 4bit 128g on WSL


This is a tutorial on how to install LLaMa on your Windows machine using WSL (Windows Subsystem for Linux).
Although with some tweaks you may get this to work properly on another hardware or on multi-GPU setups,
this tutorial is specifically designed to work with Nvidia graphics cards - and I only cover a Single-GPU configuration.
I'll be using my RTX2060 with 6GB to load Llama model 7B with 4-bit quantization,
but you can try this tutorial with other models that fit your Nvidia hardware.

----------------------------------------------------------------------------------

These instructions are delivered for educational purposes only, and it assumes that you have a fresh install of
windows 10/11 latest version (and it is obvious that you can try it without having to reinstall Windows).

While we will need to restart the Ubuntu terminal a few times, I've done my best to simplify the instructions
to minimize the number of steps. This will help you explore these AI models as fast as possible.


----------------------------------------------------------------------------------
----------------------------------------------------------------------------------

Software requirements:
----------------------------------------------------------------------------------

Open windows update (right-click on start menu; settings; update & security), click on advanced options and
enable “receive updates for other Microsoft products when you update Windows”, then
check for updates and restart your PC if required.

Go to nvidia website (or through your Geforce Experience app if u have installed) and install latest version
of your nvidia driver (make sure it is the “Game ready” version), restart again if required.

----------------------------------------------------------------------------------
----------------------------------------------------------------------------------
----------------------------------------------------------------------------------

Instructions:
----------------------------------------------------------------------------------

Click on start menu; type cmd and click on “run as administrator”

	wsl --install

It will ask to restart PC if this is the first WSL installation on this machine

After reboot WSL will continue installation...

While it does, click on start menu; type cmd and open

	notepad .wslconfig

Click on yes to create a new file; copy and paste the content below:


	[wsl2]
	memory=6GB
	processors=2
	swap=20GB
	localhostforwarding=true


Close notepad, click on save; close prompt;

When WSL installation ends, enter a username and a password


	clear && git clone https://github.com/Highlyhotgames/fast_txtgen_7B.git > /dev/null 2>&1 && cd fast_txtgen_7B && chmod +x requirements && ./requirements
	


Enter password and wait for message to close terminal; close

To ensure WSL2 is activated and to update:

Click on Start menu; type cmd and run as Administrator



	wsl --set-version Ubuntu 2 & wsl --update


Without closing prompt, open windows update and check for updates - it will get an update for WSL;

After update, go back to Admin prompt and run this line:


	cd lxss\lib & del libcuda.so & del libcuda.so.1 & wsl -e /bin/bash -c "ln -s libcuda.so.1.1 libcuda.so.1 && ln -s libcuda.so.1.1 libcuda.so" & wsl --shutdown & exit


Open Ubuntu:


	./install
	


When "checking CUDA Installation" it will display a message "release 11.7" in cyan color.


After installation you may run server:

	./run

Default URL:

—> http://127.0.0.1:7860

----------------------------------------------------------------------------------
----------------------------------------------------------------------------------
----------------------------------------------------------------------------------

To start server, open Ubuntu:

	conda activate webui && cd webui/text-generation-webui
	
Run:

	python server.py --wbits 4 --model llama-7b-4bit-128g --groupsize 128 --chat

----------------------------------------------------------------------------------
----------------------------------------------------------------------------------
----------------------------------------------------------------------------------

To remove completely (including WSL), open cmd as Admin:

	wsl --shutdown & wsl --unregister Ubuntu

----------------------------------------------------------------------------------
----------------------------------------------------------------------------------
----------------------------------------------------------------------------------
----------------------------------------------------------------------------------
