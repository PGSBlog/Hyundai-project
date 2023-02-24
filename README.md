<img src="https://capsule-render.vercel.app/api?type=Slice&color=auto&height=200&section=header&text=Hyundai-project&fontSize=90" />
<div align="center">
	<img src="https://img.shields.io/badge/Python3-007396?style=flat&logo=Java&logoColor=white" />
	<img src="https://img.shields.io/badge/RPI4-E34F26?style=flat&logo=HTML5&logoColor=white" />
	<img src="https://img.shields.io/badge/Ubuntu Server 20.04-1572B6?style=flat&logo=CSS3&logoColor=white" />
</div> 

# README
필자는 필자가 검색하여 방법론을 직접 사용해보고 테스트 성공한 내용들만 작성했습니다.

# Develop Configuration
Ubuntu-Server（20.04）　
RPI4 #gcc 9.4.0 
ROS2 Foxy 
V2.1 Camera

# RPI4에 Ubuntu-Server설치
오픈소스를 사용하기위해 Cuda, Cudnn와 연동되는 Ubuntu 20.04를 설치하려고 한다.

RPI용 Ubuntu-Server(20.04)는 [우분투 공식사이트](https://ubuntu.com/#download)에 없어서, [라즈베리파이 이미저](https://www.raspberrypi.com/software/)로 Ubuntu-Server(20.04)를 설치했다.

# Ubuntu-Server(20.04)세팅

1. 와이파이 설정
2. ssh 세팅
3. [구글링](https://pinkwink.kr/1352)，[유튜브](https://youtu.be/ah4TfDcr28I)를 보고 따라하면 된다．
4. [WIFI 세팅, 네트워크 세팅](https://velog.io/@ekdh7456/)

# V2.1 Camera연결
Ubuntu-Server는 기본적으로 raspi-config를 지원하지 않는다. V2.1 Camera를 사용하기위해 raspi-config 세팅을 해줘야한다.

==> 하지만, ROS2로 연결할거라서 다른 기본적인 세팅으로 카메라를 연결시켰다.

라즈베리파이4를 원격접속하여 /boot/config.txt를 $ source nano config.txt 해서 를 추가 한다.

>Config.txt Setting
```
start_x=1
gpu_mem=128
```

# ROS1과 ROS2차이
ROS1 = Python2.7 / Noetic(last support)

ROS1 = Python3 higher / Foxy higher 

# ROS1-Noetic설치
[ROS1-Noetic설치/환경 세팅](https://velog.io/@deep-of-machine/ROS-ROS1-%EC%84%A4%EC%B9%98-Ubuntu20.04-ROS-Noetic)

# ROS2-foxy설치
[ROS2-Foxy설치/ROS2 개발 tools설치/ROS2 환경 설정 및 단축키 관리](https://velog.io/@dbdb_dev/ROS2-ROS2-Foxy-%EC%84%A4%EC%B9%98-%EB%B0%8F-%EC%82%AD%EC%A0%9C)

# ROS2-v4l2_camera 세팅
[v4l2_camera](https://index.ros.org/r/v4l2_camera/#foxy)는 ROS1-Noetic를 지원하지 않는다. 그래서 ROS2로 설치하여 진행했다.

# ROS2-v4l2_camera [Git-Lab](https://gitlab.com/boldhearts/ros2_v4l2_camera) 테스트

# RPI4-V2.1 Camera Test

>Here is the step-by-step guide for those who'll face the same problem:
0. make sure your camera is plugged into a camera slot, not the display slot on RPI! (took me a while to notice it)

1. burn Ubuntu Server 20.04 arm 64bit image onto SD card — the image provided on the Turtlebot3 Foxy quickstart guide didn't work for me

2. connect RPI4 to display and keyboard and run through the initial setup:

- set ubuntu user password (default password is ubuntu and it asks you to reset password on first login)
- setup networking in /etc/netplan/50-cloud-init.yaml, then run sudo netplan apply. In my case, I've set up dhcp for WiFi and static IP for ethernet to be able to connect to the Turtlebot3 from my laptop.

3.make changes to /boot/firmware/config.txt by adding 2 lines at the end

>Config.txt Setting
```
start_x=1
gpu_mem=128
```
Terminal Command
```
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install v4l-utils and then sudo modprobe bcm2835-v4l2
```
> reboot and reconnect via SSH


>test that the camera now works

```
ls -l /dev | grep video 
```
should show /dev/video0

>take a picture
```
v4l2-ctl --set-fmt-video=width=2592,height=1944,pixelformat=3
v4l2-ctl --stream-mmap=3 --stream-count=1 --stream-to=somefile.jpg
```
>if the camera doesn't work at this point, you can try the following workarounds:

4. Ensure your user has access to the camera device
```
sudo usermod -aG video $USER
sudo chmod 777 /dev/vchiq
```
>Update your RPI firmware
```
sudo curl -L --output /usr/bin/rpi-update https://raw.githubusercontent.com/Hexxeh/rpi-update/master/rpi-update && sudo chmod +x /usr/bin/rpi-update
sudo rpi-update
```

> then reboot

5. After verifying that the camera works fine, follow the instructions from this thread:

6. Install additional packages for camera on both RPI and device you'll be running rviz from (a.k.a PC)
```
sudo apt install ros-foxy-image-tools
sudo apt install ros-foxy-usb-cam
sudo apt install ros-foxy-compressed-image-transport
```

7. apply changes from this PR to files in ~/turtlebot3_ws/src and then rebuild by running colcon build inside ~/turtlebot_ws

8. [위 내용은 커뮤니티 댓글에 작성되어 있다.](https://github.com/ROBOTIS-GIT/turtlebot3/issues/863)

# OpenCV YOLO object detection with PiCamera and ROS2 
>[다음에 해야할 일](https://robofoundry.medium.com/opencv-yolo-object-detection-with-picamera-and-ros2-629d52cfec6)

# 짜투리
1. [한글 키보드 설정](https://velog.io/@t1won/Ubuntu-%EC%9A%B0%EB%B6%84%ED%88%AC-%ED%95%9C%EA%B8%80-%EC%9E%85%EB%A0%A5-%EB%B0%8F-%ED%95%9C%EC%98%81%ED%82%A4-%EC%84%A4%EC%A0%95)
