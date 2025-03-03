# Apollo AGV

This repository contains the source code for the Apollo AGV - a differential-drive robot designed to aid in the filming of set pieces without human camera operators.

## Prerequisites

- Docker
- ROS Image (ros:jazzy-ros-core)

## Setting Up the Development Environment

To start the container, run the following container. It mounts the folder `container_volume/` as a volume within the container, which helps in the development of the stack within the Ubuntu environment, while allowing version control to be managed from the host side.

This command also exposes port 8765 to enable listening to ROS2 topics using Foxglove Studio.

```
docker run --rm --name apollo -it -p 8765:8765 --device /dev/ttyUSB0 -v ./container_volume:/container_volume apollo-dev bash
```

To attach a new terminal to the existing container

```
docker exec -it apollo bash
```

## Prerequisites

- Install Homebrew
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- Install libusb

```
brew install libusb-compat 
```

- Start an USB/IP Server

```
git clone https://github.com/tumayt/pyusbip
cd pyusbip
python3 -m venv .venv
source .venv/bin/activate
pip install libusb1
python pyusbip
```

- Start a container to run the usb bridge:

```
docker run --rm --name apollo-usb-ip -it --privileged --pid=host apollo-dev bash
nsenter -t 1 -m
usbip list -r host.docker.internal
usbip attach -r host.docker.internal -d 2-1
```



