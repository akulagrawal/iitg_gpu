# Using IITG GPU Cluster

## Getting the access

1. You will have to go to the CSE Dept. office in the new building to get access to the GPU cluster.

2. Tell them your requirements and they will email you the instructions along with your credentials in a day or two.


## Running the code

1. Mostly, the instructions provided in the mail are sufficient.

2. You will need to use SSH (and SFTP if you wish), protocols used to access remote machines.

### Linux 

You can google how to install SSH on your Linux system, depending on the distribution you are using.
Next, you can enter the remote system using `ssh username@ip_address` from the terminal.
SFTP is used to get a user-friendly GUI interface in the form of a standard file browsing window.

### Windows

On windows, you can download and use [PuTTY](https://www.putty.org/)


## Steps to use a custom Docker Image

1. Make an account on [Dockerhub](https://hub.docker.com).

2. Link your Dockerhub account to your Github account.

3. Make a new repo on Dockerhub and Github.

4. Open the new repo on Dockerhub and link it to the Github repo to enable the autobuild.

5. Write the Dockerfile and save locally: For this, you can learn how to write a Dockerfile by a simple google search, or else, simply download the Dockerfile from this repository and make required changes.

6. There are two methods to do this, but I doubt anyone uses method 2:

## Method 1 (Recommended)

Push the Dockerfile to the Github repo: The corresponding Docker image will start building in the Dockerhub automatically. You can verify the same by opening the repo in Dockerhub.

## Method 2

In the directory where the Dockerfile is present in the local system, enter the following commands:

  - `docker build -t <tag> .`

  - `docker login -u <docker_username>`

  - `docker tag <tag> <docker_username>/<docker_repo>:<tag>`

  - `docker push <docker_username>/<docker_repo>:<tag>`

<br />

7. After step 6 is complete, in the Dockerhub repo, you can see the final docker image under "Tags".

8. On the top right corner of the image, there will be the text to be copied of the form `docker pull <docker_username>/<docker_repo>:latest`.

9. `<docker_username>/<docker_repo>:latest` is the link to the final image. Copy the same, and replace the default image link (`abhipec/iitg_kubernetes:p3_master_image_latest`) in the .yaml file (probably `pod-creation_direct_execution.yaml`) by your link.

10. You are good to go!

## Things to Remember

1. One common mistake is that all file paths need to be updated. The file paths need to be absolute, and the default mount path is `/data/`. Thus, if I create a file `test.txt` in the same directory that opens after ssh, the location of the file in code should be `/data/test.txt`

2. Remember that the CSE Dept. GPU drivers are not updated currently, hence, some updated Docker images might not work. To tackle this issue, you may go to the Dockerhub repo of that particular program, and choose the docker image of an older version on your Dockerfile.

For eg. `tensorflow/tensorflow:latest-gpu-py3` image doesn't seem to work. Hence, use `tensorflow/tensorflow:custom-op-ubuntu16` instead.

<br />

# Please feel free to reach out to me to give suggestions and improvements.