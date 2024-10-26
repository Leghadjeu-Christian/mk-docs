# ***Running docker instance from multipass VM tool.***


This is about an overview of virtual machines (specifically *multipass*) and containers (like *docker* ) and how to run a *Docker* container on the *multipass* virtual machine to render a host machine secured, and avoid data loss.

## **Diving into the Details of the implementation**
 the removal of the docker desktop app from the MACOS for Macbooks users to avoid being used to the Graphical interface and be friendly with the execution of Docker container from the terminal 
 
To uninstall Docker Desktop from your Mac:
- From the Docker menu, select the Troubleshoot icon in the top-right corner of Docker Dashboard and then select Uninstall.
Select Uninstall to confirm your selection.

You can also uninstall Docker Desktop from the CLI. Run :
```sh
$ /Applications/Docker.app/Contents/MacOS/uninstall
```
After uninstalling Docker Desktop, there may be some residual files left behind which you can remove:
```sh
$ rm -rf ~/Library/Group\ Containers/group.com.docker
$ rm -rf ~/Library/Containers/com.docker.docker
$ rm -rf ~/.docker
```
To ensure the removal of all docker files created in the system, run the following command :
```sh
$ rm -rf docker* ~/usr/bin
```

- The corresponding steps to remove Docker container on ubuntu is as follows;
To remove Docker Desktop for Ubuntu, run:
```sh
$ sudo apt remove docker-desktop
```
Running the docker command we should have this output :
```sh 
  command not found: docker
```

- After removing Docker container tool on your host machine, the next step is to launch docker container image from the multipass virtual machine.

 This can be done by running the following command : 
```sh
$ multipass launch docker --name <name of the docker image>
```
 In our example we are going to give the name of our docker instance to be docker-vm. So we run the ```multipass launch docker --name docker-vm``` command.


ext  after launching docker from the Virtual machine ( using the multipass virtual machine tool), to run a **docker** command on your hostmachine so that it should be executed from the Virtual machine, we use the following command :
 ```sh
$ multipass exec docker-vm -- docker ps
```
## Aliasing the *docker* command.
Aliasing the docker command is all about configuring the *docker* command in such a way that when executed on the host command it will instead execute the ```multipass exec docker-vm -- docker ``` command in the virtual machine, thus making it possible to run programs in the container now found in our virtual machine, rendering our host machine safe.
This can be done using the following command :
```sh 
 alias docker="multipass exec docker-vm -- docker" 
 ```
 Now every time we type the ```docker``` command, the ```multipass exec docker-vm -- docker ``` command is executed (which saves time and increases effectiveness).

- *NOTE*: Note running this alias command will alias the *docker* command only in the terminal session you are currently into, that is when you will open a new terminal the docker command will prompt an error message, to solve this problem, we need to add the alias line to a shell configuration file like the **~/.zshrc** or  **~/.bashrc** depending on your default shell.
## Aliasing the docker command into the shell configuration file.
Aliasing the docker command into the shell configuration file is all about making the docker command available every time we open the terminal.
This is done by following the steps below :
- Open the shell configuration file to edit it, with a text editor. Run the command:
``` nano ~/.zshrc``` (this depends on the default installed shell, it could be .bashrc file ).
-  Scroll to the end of the file, then to the extreme empty line of the file add the following line;
``` alias docker="multipass exec docker-vm -- docker"```
- Then save the file modifications with th ```ctrl+o``` -key then ```ctrl+x``` to exit the file.
- Next source the file to print its output to the terminal, so as to implement the modifications made in the .zshrc file by running the ```source ~/.zshrc``` command.
Now that the modifications have been implimented on the termnal, we can type the ```docker``` command to verify that the alias has been applied. 
 
 Hope this solutions helped you, don't hesitate to navigate through my repositories.
 See you !!