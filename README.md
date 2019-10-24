### IvLabs PC and GPUs Usage Guidelines 
      _____     _           _         
     |_   _|   | |         | |        
       | |_   _| |     __ _| |__  ___ 
       | \ \ / / |    / _' | '_ \/ __|
      _| |\ V /| |___| (_| | |_) \__ \
      \___/\_/ \_____/\__,_|_.__/|___/

Welcome to the IvLabs PC. If you are on this page, chances are you have just been given access to the PC.
Follow the rules for using this PC at [https://tiny.cc/IvLabs_PC_Rules](https://tiny.cc/IvLabs_PC_Rules).
Before using any GPU, you must book it in [http://tiny.cc/IvLabsGPUs](http://tiny.cc/IvLabsGPUs).
If you don't understand how to use things, contact the admin on the Discord channel #gpus.

#### GPUs and other resources
- Keep usage of resources under control. For RAM and cores usage : `htop` and for GPU usage : `nvidia-smi`
- After running your code (in case it is not stable), make sure that resources being used are under control (using above commands).
- To use a GPU, you must first book it at this [this address](http://tiny.cc/IvLabsGPUs), you will find some rules on how to do it in the spreadsheet. If you have any questions, please ask!
- In case you have to login using the monitor in lab, then remember to log out before leaving. This is necessary since logging in at the monitor will take up GPU memory which is not released even when the monitor is switched off.
- Use at most one GPU at a time. In case you need more, use the Discord #gpus channel to ask for permission and coordinate with the other users.
     - By default, TensorFlow uses all GPUs available. Set up your experiments to use the correct GPU.
     - In PyTorch, use `torch.cuda.set_device(id)` to set the proper GPU. Replace `id` with `0` for GPU0 and so on.
- After completing your task make sure you release the GPU memory (if not done automatically). Use `nvidia-smi` to look at running processes and kill them using `kill <pid>`.
- To determine the owner of process `<pid>`, use `ps -o user= -p <pid>` to find the username of the owner. If GPU is not booked, use the #gpus channel on Discord to coordinate with the user or request the admin to kill the process. If unbooked GPU user does not respond quickly, then admin must kill the process.

#### How to setup your enviroment
- You must use conda to create an enviroment if you have custom dependencies for your project. DO **NOT** install conflicting packages in the base enviroment.
- Useful conda commands are listed below 
     - To create an enviroment: `conda create -n <name_of_your_enviroment>` 
     - Enviroment with custom Python version: `conda create -n <name_of_your_enviroment> python=X.X` where `X.X` represents the Python version you want to install. For example, the command for creating an enviroment with Python 3.5 would look like: `conda create -n <name_of_your_enviroment> python=3.5`
     - To install custom packages while creating your envrioment you can just list them out like this: 
          ```
          conda create -n <name_of_your_enviroment> <package1> <package2>
          ``` 
          e.g. for creating enviroment with `pip` and `sklearn` packages the command would be: `conda create -n <name_of_your_enviroment> pip sklearn` *Note: You can install `pip` as a conda package and then use it to install other packages as well*
     - **Make sure you are within your own environment** and then you can use `conda` to install packages: `conda install <package_name>`, if the package is on custom channel use: `conda install -c <channel_name> <package_name>`
     - For more information on how to use conda please refer to the [conda official documentation](https://docs.conda.io/en/latest/).

#### Writing code over ssh
- Jupyter Lab / Notebook :
     - Start Jupyter Notebook / Lab using `jupyter-lab --port=<allocated_port> --no-browser` after logging into your account.
     - In a local terminal, use `ssh -f -N -L localhost:<local_port>:localhost:<allocated_port> username@ip_address` to forward the `allocated_port` to your `local_port`.
     - Note that `local_port` and `allocated_port` are 4-digit numbers. Also, if either of the ports is already in use, the above command may fail.
     - Open the browser in your local PC and type URL `localhost:<local_port>`.
     - For installing anaconda enviroments in jupyter use the following commands
     ```
     source activate myenv
     python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
     ``` 
     for more info refer [link](https://stackoverflow.com/questions/39604271/conda-environments-not-showing-up-in-jupyter-notebook)
- Visual Studio Code : 
     - This is one of the easiest ways to remotely write code.
     - Just follow the instructions given [here](https://code.visualstudio.com/docs/remote/ssh) and you can setup VS Code to connect to the remote server and edit any files there. 
     - Using key-based authentication, you can configure both your laptop terminal and VS Code to login without password. Instructions for that are linked in the previous link.
- PyCharm or Atom or other editors :
     - There may be ways to configure a remote server on these editors too. If someone finds the link to instructions for this, then you can open a pull request linking it here or contact the admins to add it here.
- Vim / Nano :
     - `vim` and `nano` are terminal-based text editors which can also be used for quick access.
     
#### Using GUI applications over ssh with X11 forwarding
- The requirements for the server side are already setup by the admin.
- On your own Ubuntu machine, while logging in, use `ssh -X username@ip_address`.
- To make X11 forwarding default in your machine, add `ForwardX11 yes` in the `~/.ssh/config` file in your local machine.
- Then, any GUI application can be started on the remote server (using the usual commands) and the display will be shown on your local machine.

#### Using ROS and ROS based applications
- ROS has already been installed system-wide. However, ROS environment variables will not be sourced by default in your bash terminals (since `source /opt/ros/kinetic/setup.bash` hasn't been added to the `.bashrc` file of the root user). 
- Thus, to use ROS, you must do `source /opt/ros/kinetic/setup.bash` in each terminal that you wish to use for ROS related commands. To make it default to your user (NOT the root user), you may add this command to your user's `.bashrc` file (this file is present in your home folder. If you're unsure, you can contact the admin on #gpus channel on Discord).
- Note that there is no need to use the monitor in the lab for ROS based applications. You can do your work through ssh, and follow the X11 forwarding instructions above to get GUI applications working through ssh. 
- **WARNING**: If you add the source command to your `.bashrc` file, then you risk conflicts between your dependencies and dependencies in your `conda` or other environments (if any). So, if you face conflicts in (say) OpenCV (this is the most common conflict), then be sure to check your `.bashrc` file.
- **WARNING**: Your simulations may lag when any training is going on (since CPU is also used during training). So, check if training is going on using `watch nvidia-smi` and coordinate with other users on the #gpus channel on Discord.

**Instruction to current and future Admins**: Never put the source command in the root user's `.bashrc` file. It will create conflicts for other users' environments who don't use ROS.

#### How to launch experiments
- Use `tmux` to keep the session active even when you are disconnected from the server.
If you haven't used it before, read [this tutorial](https://linuxize.com/post/getting-started-with-tmux/) to learn all the basics and [this cheatsheet](https://gist.github.com/MohamedAlaa/2961058) for some advanced functionalities.
- Run the program or start the Jupyter Notebook / Lab within the tmux session.
- Use the `watch nvidia-smi` command to monitor GPU usage.
- Use `htop` to keep resources under control.
- If other users are already using for training or running simulations or other tasks, then coordinate with them on the #gpus channel on Discord. 
