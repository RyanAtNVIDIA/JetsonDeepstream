# JetsonDeepstream
For setting up an NVIDIA Jetson with Deepstream

## Initial Jetpack Install
I have found it is easies to flash a new MicroSD card image for every project. The steps to flash jetpack onto a MicroSD card can be found here: https://developer.nvidia.com/embedded/jetpack


## Setting up to run Deepstream container
1) Create a "my_apps" directory
```mkdir -p ~/my_apps```
2) Create a reusable script
Create a bash script file.
```
echo "sudo docker run --runtime nvidia -it --rm --network host \
    -v /tmp/.X11-unix/:/tmp/.X11-unix \
    -v /tmp/argus_socket:/tmp/argus_socket \
    -v ~/my_apps:/dli/task/my_apps \
    --device /dev/video0 \
    nvcr.io/nvidia/dli/dli-nano-deepstream:v2.0.0-DS6.0.1 " > ds_docker_run.sh
 ```
 Make it executable
 ```chmod +x ds_docker_run.sh```
 3) Launching the container
 The first time the container tries to launch it will need to download it from NVIDIA's NGC
 ```./ds_docker_run.sh```
