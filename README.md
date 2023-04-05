# Installation Script for LLaMa 7B 4bit 128g on WSL


	This is a tutorial on how to install LLaMa on your Windows machine using WSL (Windows Subsystem for Linux). Although with some tweaks you may get this to work properly on another hardware or on multi-GPU setups, this tutorial is specifically designed to work with Nvidia graphics cards - and I only cover a Single-GPU configuration. I'll be using my RTX2060 with 6GB to load Llama model 7B with 4-bit quantization, but you can try this tutorial with other models that fit your Nvidia hardware.

	These instructions are delivered for educational purposes only, and it assumes that you have a fresh install of windows 10/11 latest version (and it is obvious that you can try it without having to reinstall Windows).

	While we will need to restart the Ubuntu terminal a few times, I've done my best to simplify the instructions to minimize the number of steps. This will help you explore these AI models as fast as possible.

	Whenever you find a command line saying "git reset..." you can skip those commands by deleting them below if you want to try the latest versions; I have inserted those lines to maximize compatibility throughout time.



Software requirements:


	Open windows update (right-click on start menu; settings; update & security), click on advanced options and enable “receive updates for other Microsoft products when you update Windows”, then check for updates and restart your PC if required.

	Go to nvidia website (or through your Geforce Experience app if u have installed) and install latest version of your nvidia driver (make sure it is the “Game ready” version), restart again if required.



Instructions:


—> Start menu —> type cmd and click on “run as administrator”

—> wsl --install

(restart PC; while WSL continues installation, start menu; type cmd and open)

—> notepad .wslconfig

(click on yes to create a new file; copy and paste the content below)


[wsl2]
memory=6GB
processors=2
swap=20GB
localhostforwarding=true


(close notepad, click on save; close prompt)

(when WSL installation ends, enter a new username and pwd)


—> git clone https://github.com/Highlyhotgames/txtgen.git && cd txtgen && chmod +x requirements.run && chmod +x install.run && ./requirements.run


(enter pwd; after insert line, wait for message to close terminal)

(start menu; type cmd and run as Administrator)

(to ensure WSL2 is activated and to update:)


—> wsl --set-version Ubuntu 2 & wsl --update


(without closing prompt: start menu; right-click on Ubuntu; more -> pin to taskbar; open windows update and check for updates - it will get an update for WSL, after that go back to Admin prompt:


—> cd lxss\lib & del libcuda.so & del libcuda.so.1 & wsl -e /bin/bash -c "ln -s libcuda.so.1.1 libcuda.so.1 && ln -s libcuda.so.1.1 libcuda.so"


(close prompt; wait 8s; open Ubuntu)


—> cd txtgen && ./install.run


	Need to input password to install CUDA. You should see "release 11.7" in cyan color after CUDA install.


	After model completes loading, if you see a last line saying "To create a public link, set `share=True` in `launch()`.", then you can open your browser and enter this URL:


—> http://127.0.0.1:7860





	Enjoy!






