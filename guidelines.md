### IvLabs PC and GPUs Usage Guidelines

#### GPUs and other resources
- Keep usage of resources under control. For RAM and cores usage : `htop` and for GPU usage : `nvidia-smi`
- After running your code (in case it is not stable), make sure that resources being used are under control (using above commands).
- To use a GPU, you must first book it at this [this address](http://tiny.cc/IvLabsGPUs), you will find some rules on how to do it in the spreadsheet. If you have any questions, please ask!
- Use at most one GPU at a time. In case you need more, use the Discord #gpus channel to ask for permission and coordinate with the other users.
- By default, TensorFlow uses all GPUs available. Set up your experiments to use the correct GPU.

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
