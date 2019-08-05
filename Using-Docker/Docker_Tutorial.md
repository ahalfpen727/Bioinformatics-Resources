# Docker Tutorial

This tutorial is designed to instruct new members in how to use [the Docker system][docker]. While the actual [Docker documentation][docs] is quite good, we have written out some extra details to supplement your knowledge of the Docker system. Though this tutorial will not go into all the details of how Docker works, it will provide all the essential information both to use Docker images and to build independent Docker images.

### What is Docker?

Put simply, Docker is a container-based system that allows you to run applications or sequences of applications independent from the resources and other programs on your operating system. Docker containers are self-contained, meaning that all the file dependencies, system libraries, and runtimes required for running an application are already included in the container. The only thing that a Docker container actually shares with the local computing system is the kernel; consequently, Docker is very lightweight. Because of this property, Docker image downloads are very efficient, they can start instantly, and you can potentially run multiple containers in parallel on a single system. Also, since the particular libraries are already included in a Docker container, source code variance among machines is eliminated and program outputs are reproducible. Different environments, same results. This reproducibility is especially useful in scientific computing given the need for consistency in results.

### Docker vs. a typical virtual machine

For those who are experienced in this area, this description of Docker may sound a lot like a typical virtual machine. For those who are unfamiliar with the term, a *virtual machine (or VM)* is an emulator for a particular operating system (OS). The emulation allows for a computer program to mimic another operating system's hardware so you can run dedicated software on the virtual machine rather than the default OS. A virtual machine is typically isolated from the original OS, but its resources are limited to those of the machine on which it is running. 

The key difference between the container model and a full-on virtual machine lies in what exactly is being virtualized or emulated. While a VM virtualizes an operating system in its entirety, along with the necessary interface, containers only virtualize *calls* to said operating system. Both are independent of the local system, just in different ways. A virtual machine is independent in the sense of being entirely isolated from the original OS and being limited in its capacity to share resources with other processes; however, it is relatively resource-intensive. In contrast, a container is much less demanding in resources (i.e. it is lightweight) and it shares resources more easily, but it is less isolated since there is some degree of connection to the original OS kernel.

Which is best? Depends on your needs. If you only needs to run individual applications or to run many applications in parallel, then a container system like Docker may be the better choice. Otherwise, if you need guaranteed resources, a greater degree of isolation, or to run entire workflows rather than single applications, you may benefit from using a VM.

### Installing Docker

First, if you are using a Linux OS, your installation instructions for Docker will be slightly different. Consult [the instructions on the official Docker website](https://docs.docker.com/engine/installation/ubuntulinux/) to learn the installation method. Furthermore, you will be able to skip the section on using a Linux virtual machine, and the section on mounting folders to the virtual machine (since you will be running Docker directly on your system).

If you are using either a Windows or Mac OS, you will need to download the Docker Toolbox from [the official website.][toolbox] The Docker Toolbox contains everything necessary to get started using Docker, including:

* **Docker client:** The actual Docker executable that is run on your computer. This is configured by Docker Machine to actually communicate with the host so applications can be run.
* **Virtualbox:** A program for creating the Linux virtual machines necessary to run Docker images. Works for both Windows and Mac.
* **Docker Machine:** The actual program for installing Docker on your local system, setting up the Docker engine on the host machine, and configuring the local Docker client for communicating with the host.
* **Docker Compose:** Program for packing together multi-container or distributed applications into a single file. This practice allows you to run the compacted application sequence as a single command.
* **Docker Kitematic:** A nice graphic user interface (GUI) for accessing the [Docker Hub][docker-hub] and perusing through new Docker images to download.

Once you have finished installing the Docker toolbox, you will be ready to start. To see all the commands available, type `docker -h`.

### Accessing Docker

First, access the Docker executable from your menu. From here, the terminal/command prompt will appear and connect to the Docker client. Once the whale icon appears, everything is loaded; however, traditional Docker commands will not work from this screen. Why? Docker is a strictly Linux-based software, so to run it on a non-Linux OS, Docker requires an extra layer of abstraction between the local OS and the Docker container. This is where the VirtualBox software comes in. As mentioned previously, VirtualBox sets up a virtual machine designed to emulate a Linux OS on which Docker containers can run; therefore, you can simply connect to the virtual machine and run Docker from there. 

To access the host from which the actual Docker images are run, type in the command `docker-machine ssh <virtual machine name>`. From personal experience, the name for the starting virtual machine is `default`, but depending on your VirtualBox settings the name may be different. This command will set up a secure shell channel to remotely login to the Linux virtual machine. Like the local Docker client, a whale icon will appear once you have successfully logged in, and from here, all the Docker commands can be run without issue.

### Pulling a Docker container

The first thing to do once logged into the VM is to pull a Docker container. To start, we suggest choosing something simple. One good start image to download is the *hello-world* image which verifies that Docker is working on the system. To download, or "pull" a Docker image, type `docker pull <container name>`. In this case, run the command `docker pull hello-world`. By default, Docker will download the latest version of the image unless specified otherwise with a particular tag. For future reference, downloading a particular version, say, of this hello-world image would take the command `docker pull hello-world:<version name>`. Note that there will be multiple lines indicating that multiple parts are being downloaded. This is due to the layered nature of Docker images, and we will explain this in more depth in the section on creating Docker images.

### Running a Docker image

Now that the *hello-world* image has been downloaded, we will need to run it. To do so, just type `docker run hello-world` into the command line. If the run was successful, you should see this:

![hello world](docker-helloworld.JPG)

Now that the Docker machine is working, we can try something slightly more advanced. Pull the ubuntu image using a similar command: `docker pull ubuntu`. Again, since this image does not exist on the host by default, it will require a few minutes to fully download. Once the image is downloaded, we're going to try something a little different. This time, type `docker run -t -i ubuntu /bin/bash`. Let's break this command down a little bit:

* The `docker run` part should be a little familiar, since we just used it with the *hello-world* image! This is just the default command for running a Docker image.
* The `-t` flag tells Docker to select an image by its tag rather than by its alphanumerical ID (which may be substantially harder to remember)
* The `-i` flag tells Docker to run the container in interactive mode. This means that Docker will connect to the container's stdin (standard input; stream data going into a program). Because this particular container is being run in interactive mode, any commands typed after the image tag/ID will be treated as commands sent to the container itself.
* `/bin/bash` the actual command that will be run on the ubuntu container. The /bin/bash command goes straight to the root directory of the container, where you may navigate through it as you would a typical Linux terminal.

A method for running containers in the background is by using *daemon mode*. To run a container in daemon mode, use the `-d` flag. For example, running a loop in the ubuntu image in daemon mode would look like so:
`docker run -d ubuntu:latest /bin/sh -c "while true; do echo hello world; sleep 1; done"`. The output for this command will be a long string. Where's our normal output? It's actually in this string. This string is actually a container ID for the ubuntu container we've run. Now we can check our active containers with the `docker ps` command, and sure enough, the first container in the list matches the ID we got as output. 

Furthermore, we can look inside the container with the `docker logs` command. Typing in `docker logs <container ID>`, we get a output that looks a lot like this:

![logs](docker_logs.JPG)

### Containers vs. Images

By now, it may seem as if the terms Docker *container* and Docker *image* are being used interchangeably throughout this tutorial; however, they are two distinct concepts. A Docker image is the complete application bundle with source code and dependencies that you download or pull from Docker Hub. A Docker container is particular copy of an image that you run on your local system. Comparing it to iPlant's Atmosphere system, think of a general Atmosphere image as comparable to a Docker container. Similarly, a specific Atmosphere instance is like a Docker container run on a local system or a host VM. 

### Listing Containers

To list all the images that you have downloaded, type `docker images`. Here, details about each image such as the particular version, the full name of the image, and the date/time when the image was downloaded. To see all the Docker containers you have set up, either active or inactive, type `docker ps -a`. By default, the `docker ps` command will list out only the containers you have active, but the `-a` flag will indicate to list all the containers. Similarly, the `ps` command will show the containers, their version, the alphanumerical ID, and the time since the container was created.

### Removing Containers

To remove an existing container that you have pulled/downloaded from Docker Hub, type the command `docker rm <container ID>`. Should an error be produced, either due to conflicts or technical difficulties, the force flag `-f` may be used to force the deletion of a given container. For an image, you will use the command `docker rmi <container ID>`. Similarly, errors here will most likely be as a result of an active container referencing the image with the given ID or tag. Here again, you may use the force flag `-f` to force the deletion of all images referring to said ID. 

### Mounting data onto a container

##### Mounting a Folder onto the VM
In all probability, the application that you want to run with Docker requires some kind of data as input. Fortunately, mounting data onto a Docker container is simple once you know what to do. First, since Docker only communicates directly with the Linux VM rather than your actual operating system, you will need to connect the local files/directories you want to use as input to the virtual machine. Do this by loading the VirtualBox program, clicking the **Settings** button, and choosing the **Shared Folders** entry in the sidebar. Here, click the *Add Shared Folder* button and just navigate to the folder you want to have mounted on the virtual machine. Once the folder has been selected, you may right-click on it's name in the list to edit its properties (e.g. access permissions, whether or not to automatically mount it onto the machine). Note that the file will now be available on the Linux VM once you connect to it. Just navigate to the root directory and you will see a folder `/c/` listed. That is your mounted folder right in the root directory!

##### Mounting Input Files

To mount a particular file when running a Docker container (e.g. for data input), please note that you must be aware of the location of the file on the Linux VM. You can mount a given file on a Docker image by using the `-v` flag, the full path to the file on the Linux VM, and the "alias path" that the file will take on the Docker image. For example, given the input file `/home/test/file1` on a Linux VM, we wanted to mount this to an alias path `/usr/file1` so we could run it through our application `analysisProgram`. In this case, we would mount it on a Docker image when running a program like so:

`docker run -v /home/test/file1:/usr/file1 -t -i analysisProgram `

Note that the actual file path and the alias path are always separated by a colon. Multiple files and even entire folders/directories can be mounted at once, they just need to be separated by another `-v` flag. So if we had another file `/home/test/file2` that we wanted to mount as well...

`docker run -v /home/test/file1:/usr/file1 -v /home/test/file2:/usr/file2 -t -i analysisProgram `

...then this command above will do the trick.

### Creating a Docker image

Creating a Docker image is fortunately not as hard as you might think it is. The key method for creating a Docker image is by using a file, known as a *Dockerfile*, to run a series of commands for describing and setting up an image. Let's take a look at a basic example of a Dockerfile:

![dockerfile](Dockerfile_pic.JPG)

Now let's take a look at some of these commands and what they mean:
* `FROM`: (optional) An image name and tag. Allows you to use an existing Docker image as a base for the new image. All of the subsequent commands in the file will be commands run on this image
* `RUN`: runs a command on the docker image. You may think of this as if you were inputting the command onto a Linux terminal. Whatever is run here takes place on the Docker image, rather than the local system.
* `COPY`: transfers a file from your local system onto the image in the desired location. Typically, the format for this line will be `COPY <file to be transferred> <directory for transferred file>`. A similar command, `ADD`, may also be used to transfer files, but typically using `COPY` is the best practice since it is more transparent and does not have any obscured features like `ADD` does.
* `WORKDIR`: Establishes the working directory for the Docker image. If any commands are run after the working directory is set, those commands will run in said working directory. Also, should this be the last command in the Dockerfile (as in the example here), then said directory will be the default directory the image opens to anytime the `docker run` command is entered.

There are, of course, more commands at your disposal for your Dockerfile, but these four are the main commands that you will most likely use in creating a Docker image. For the full list of commands, [check here][commands]

Once you have your Dockerfile built, save it under just the name *Dockerfile*, **without any file extension!** The Docker client looks only for a file actually named Dockerfile, so if it has an extension, it will produce an error. When the file is done, be sure it is in the same directory with whatever file(s) you wish to copy onto the image. Then, be sure said directory is mounted on the virtual machine and use the `cd` command (for **c**hange **d**irectory) to move to the same directory where the Dockerfile and accompanying files are. Next, type the docker build command:
`docker build -t <image name> .` The Docker terminal will then start building the image. 

![dockerbuild](dockerbuild.JPG)

Note that each step produces a container ID. This is because Docker has a layered nature in building images. Basically, think a Docker image like a layered cake where each command is like a new layer stacked on top of the foundation of the original image. All of these layers are treated like their own separate intermediate images with their own image IDs. Once all the commands or "layers" of the image are set up, the intermediate images are deleted, leaving only the final image and its final ID. Now you can push it onto Docker Hub for public use.

To push an image onto Docker Hub, be sure to make an account on the [main Docker Hub page.][docker-hub] Once that's done, go back to the Docker terminal and Linux VM. Type the `docker login` command, enter your credentials, and then you may push the image to your Docker Hub account with `docker push <container ID>`.
   
   [docker]: <https://www.docker.com/>
   [docs]: <https://docs.docker.com/>
   [toolbox]: <https://www.docker.com/docker-toolbox>
   [docker-hub]: <https://hub.docker.com/>
   [commands]: <https://docs.docker.com/v1.8/reference/builder/>
