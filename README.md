### IvLabs PC and GPUs Usage Guidelines 

#### GPUs and other resources
- Keep usage of resources under control. For RAM and cores usage : `htop` and for GPU usage : `nvidia-smi`
- After running your code (in case it is not stable), make sure that resources being used are under control (using above commands).
- To use a GPU, you must first book it at this [this address](http://tiny.cc/IvLabsGPUs), you will find some rules on how to do it in the spreadsheet. If you have any questions, please ask!
- Use at most one GPU at a time. In case you need more, use the Discord #gpus channel to ask for permission and coordinate with the other users.
- By default, TensorFlow uses all GPUs available. Set up your experiments to use the correct GPU.
- After completing your task make sure you release the GPU memory (if not done automatically). Use `nvidia-smi` to check for processes and kill them using `kill <pid>`. 

#### How to setup your enviroment
- You must use conda to create an enviroment if you have custom dependencies for your project. DO **NOT** install conflicting packages in the base enviroment.
- Useful conda commands are listed below 
     - To create an enviroment: `conda create -n <name_of_your_enviroment>` 
     - Enviroment with custom Python version: `conda create -n <name_of_your_enviroment> python=X.X` where `X.X` represents the python version you want to install. For example command for creating an enviroment with Python 3.5 would look like: `conda create -n <name_of_your_enviroment> python=3.5`
     - To install custom packages while creating your envrioment you can just list them out like this: 
          ```
          conda create -n <name_of_your_enviroment> <package1> <package2>
          ``` 
          e.g. for creating enviroment with `pip` and `sklearn` packages the command would be: `conda create -n <name_of_your_enviroment> pip sklearn` *Note: You can install `pip` as a conda package and then use it to install other packages as well*
     - You can use `conda` to install packages: `conda install <package_name>`, if the package is on custom channel use: `conda install -c <channel_name> <package_name>`
     - For more information on how to use conda please refer to the [conda official documentation](https://docs.conda.io/en/latest/).

#### Writing code over ssh
- Jupyter Lab / Notebook :
     - Start Jupyter Notebook / Lab using `jupyter-lab --port=<allocated_port> --no-browser` after logging into your account.
     - In a local terminal, use `ssh -f -N -L localhost:<allocated_port>:localhost:<local_port> username@ip_address` to forward the `allocated_port` to your `local_port`.
     - Note that `local_port` and `allocated_port` are 4-digit numbers. Also, if either of the ports is already in use, the above command may fail.
     - Open the browser in your local PC and type URL `localhost:<local_port>`.
- PyCharm or Atom or other editors :
     - There are ways to configure a remote server on such editors. But it is tedious to find instructions for each and everyone.
- Vim / Nano :
     - `vim` and `nano` are terminal-based text editors which can also be used.
     
#### How to launch experiments
- Use `tmux` to keep the session active even when you are disconnected from the server.
If you haven't used it before, read [this tutorial](https://linuxize.com/post/getting-started-with-tmux/) to learn all the basics and [this cheatsheet](https://gist.github.com/MohamedAlaa/2961058) for some advanced functionalities.
- Run the program or start the Jupyter Notebook / Lab within the tmux session.
- Use the `watch nvidia-smi` command to monitor GPU usage.
- Use `htop` to keep resources under control.
