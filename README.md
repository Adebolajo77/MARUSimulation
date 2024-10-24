# MARUSimulation


## Host machine 

https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html

```shell
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

sed -i -e '/experimental/ s/^#//g' /etc/apt/sources.list.d/nvidia-container-toolkit.list

sudo apt-get update

sudo apt-get install -y nvidia-container-toolkit

sudo nvidia-ctk runtime configure --runtime=docker

sudo systemctl restart docker

```


## installations 

```shell

git clone https://github.com/MARUSimulator/marus-docker.git

cd marus-docker

xhost +

## both private and public key files must be present 
## you add your public key to your github repo 

sudo docker build -t marus_docker . --build-arg ssh_prv_key="$(cat ~/.ssh/id_rsa)" --build-arg ssh_pub_key="$(cat ~/.ssh/id_rsa.pub)"


docker run --rm -v /tmp/.X11-unix:/tmp/.X11-unix --gpus all --runtime nvidia -e DISPLAY=$DISPLAY --privileged -it marus_docker /bin/bash


```
## testing 

```shell

ros2 launch grpc_ros_adapter ros2_server_launch.py

```


```shell

unityhub

## login or sigup

add marus_example project (/home/marus_user/marus_example).

```

