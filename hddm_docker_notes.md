Repo for the hddm docker image

https://github.com/hcp4715/dockerHDDM

# Running a container with access to local jupyter notebooks

Command to run HDDM interactively. To access local notebooks run from/mount directory containing the nb's.  

```
docker run --rm -it -v ${PWD}:/home/jovyan/work -p 8888:8888 hcp4715/hddm:0.9.8 jupyter notebook
```

# Running multiple containers mounted on different directories

Note, if you want to run multiple containers from different directories you should expose the container to a different local port.  

The container will listen on port `8888` for the internal jupyter nb command but you can/should expose it to another local port so it do  

So your commands would looks like:  

```
docker run --rm -it -v ${PWD}:/home/jovyan/work -p 8787:8888 hcp4715/hddm:0.9.8 jupyter notebook
```

Notice that the local port is different than the port inside the container after the colon (similar syntax to when mounting directories)  

The output of this command will be similar to the previous one listing the local port at 8888  

```
    To access the notebook, open this file in a browser:
        file:///home/jovyan/.local/share/jupyter/runtime/nbserver-7-open.html
    Or copy and paste one of these URLs:
        http://8cadbcf1437f:8888/?token=<YOUR-RANDOM-TOKEN>
     or http://127.0.0.1:8888/?token=<YOUR-RANDOM-TOKEN>
```

*BUT* now in your browser you'd need to navigate to `http://127.0.0.1:8787/tree/work` instead of `http://127.0.0.1:8888/tree/work` to connect to the directory you mounted onto the second container.