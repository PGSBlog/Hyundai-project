<img src="https://capsule-render.vercel.app/api?type=Slice&color=auto&height=200&section=header&text=Hyundai-project&fontSize=90" />
<div align="center">
	<img src="https://img.shields.io/badge/Python3-007396?style=flat&logo=Java&logoColor=white" />
	<img src="https://img.shields.io/badge/RPI4-E34F26?style=flat&logo=HTML5&logoColor=white" />
	<img src="https://img.shields.io/badge/Ubuntu Server 20.04-1572B6?style=flat&logo=CSS3&logoColor=white" />
</div> 

<h3>개발환경</h3>
 
 #Ubuntu-Server（20.04）　#RPI4 #gcc 9.4.0 #ROS2 Foxy #V2.1 Camera

<h3>RPI4에 Ubuntu-Server설치</h3>

#오픈소스를 사용하기위해 Cuda, Cudnn와 연동되는 Ubuntu 20.04를 설치하려고 한다.
#RPI용 Ubuntu-Server(20.04)는 공식사이트(https://ubuntu.com/#download)에 없어서, 라즈베리파이 이미저(https://www.raspberrypi.com/software/)로 Ubuntu-Server(20.04)를 설치했다.

<h3>Ubuntu-Server(20.04)세팅</h3>
#1. 와이파이 설정
#2. ssh 세팅
#구글링(https://pinkwink.kr/1352)，유튜브(https://youtu.be/ah4TfDcr28I)를 보고 따라하면 된다．
#WIFI 세팅, 네트워크 세팅(https://velog.io/@ekdh7456/)

<h3>V2.1 Camera연결</h3>

#Ubuntu-Server는 기본적으로 raspi-config를 지원하지 않는다. V2.1 Camera를 사용하기위해 raspi-config 세팅을 해줘야한다.
#==> 하지만, ROS2로 연결할거라서 다른 기본적인 세팅으로 카메라를 연결시켰다.
#라즈베리파이4를 원격접속하여 /boot/config.txt를 $ source nano config.txt 해서 를 추가 한다.

<h3>ROS1 Noetic설치</h3>
#
<h3>ROS2 foxy설치</h3>
#https://velog.io/@ekdh7456/%EB%9D%BC%EC%A6%88%EB%B2%A0%EB%A6%AC%ED%8C%8C%EC%9D%B4-%EC%9A%B0%EB%B6%84%ED%88%AC-%EC%84%9C%EB%B2%84%EC%97%90-ROS2-foxy-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0
