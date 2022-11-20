# nvidia-dli

### 이미지 굽기
   - sd card formatter를 설치해서 sd카드 안에 있는 쓰레기 데이터를 비우고 이미지를 구울 사전준비를 한다.
   - Balena Etcher   :  Linux version Download를 다운로드해준다.
   - jetpack를 다운로드한다. (https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write)
   - 그리고 Balena Etcher를 관리자권한으로 실행해야한다. (안 그러면 실행이 되지 않을 수 있음)
   - sd카드를 굽는다

![캡처](https://user-images.githubusercontent.com/102521625/200294742-1785544a-27cd-4e3c-9fef-e60e707603c7.PNG)  

--------------------------------------------------------------------------------------------------------------  

### 젯슨나노 세팅
![JetsonNano-DevKit_Front-Top_Right_trimmed](https://user-images.githubusercontent.com/102521625/202900456-005377c2-0674-40cf-9021-8afcf58be629.jpg)
   - sd카드를 젯슨나노에 넣는다.
   - 와이파이 동글을 꽂는다.
   - 마우스와 키보드를 연결한다.
   - HDMI선으로 모니터와 젯슨나노를 연결한 뒤, 화면을 HDMI로 바꾸어준다.  

### 우분투 설치
  
  - 밑에 있는 사진을 보고 따라한다.
![1](https://user-images.githubusercontent.com/102521625/202900860-abde7082-e4ee-447f-8951-42ccd806a3a7.jpg)
  
![2](https://user-images.githubusercontent.com/102521625/202900889-0b449bd3-ca49-436f-9869-73f519c015bd.jpg)  

![3](https://user-images.githubusercontent.com/102521625/202900903-07e9b0f2-b8cf-4295-8552-04b5f1b9ad72.jpg)
  
- 그다음으로 와이파이를 설정해주고 지도에서 서울을 선택하고 다음창으로 넘어간다. 
- 그리고 다시 사진을 보고 따라하면.. 
  
![4](https://user-images.githubusercontent.com/102521625/202901012-bb1f3b66-37ef-4a2c-89e9-3c9c15f30eb4.jpg)
  
![5](https://user-images.githubusercontent.com/102521625/202901038-4b763891-a7ba-4066-9442-2e5f9a245373.jpg)
  
![6](https://user-images.githubusercontent.com/102521625/202901055-f861af5d-3f40-4ea7-ab65-acb557f2ccc7.jpg)
  
![7](https://user-images.githubusercontent.com/102521625/202901064-998fa51b-41af-4df2-acd1-e3fe7d4821e6.jpg)
  
  
![1](https://user-images.githubusercontent.com/102521625/202901130-1220753e-109a-4f1f-8412-8c4b4ee902fd.jpg)
  
- 그렇게 하고나면 이렇게 녹색화면으로 바뀌게 된다.
  
  
![2](https://user-images.githubusercontent.com/102521625/202901261-e404a9e2-54b1-4566-b455-5c5202bff301.jpg)  
- 그다음에 terminal에 들어간 뒤, 'free -m'을 써서 용량을 확인해준다. 사진에서는 스왑용량이 1GB이지만 우리는 4GB가 필요
  
![3](https://user-images.githubusercontent.com/102521625/202901460-4673a559-c05d-4d8d-bf11-5e20e31bd9e6.jpg)
- 위에 있는 명령어를 치고나면  
# Disable ZRAM:
sudo systemctl disable nvzramconfig

# Create 4GB swap file
sudo fallocate -l 4G /mnt/4GB.swap
sudo chmod 600 /mnt/4GB.swap
sudo mkswap /mnt/4GB.swap

# Append the following line to /etc/fstab
sudo echo "/mnt/4GB.swap swap swap defaults 0 0" >> /etc/fstab


![4](https://user-images.githubusercontent.com/102521625/202901583-06260127-467e-4a9b-a759-f88843453c87.jpg)
- 위에와 같은 화면이 나오는데 여기서 사진에 있는 마지막 한줄을 쳐주게되면 스왑이 된 것이다.  
- 여기서 창을 닫기 위해서 ':wq'라는 명령어를 쳐서 닫고 다시 'free -m'을 쳐서 확인한다.  
- 하지만 여기서 아직도 용량이 변하지 않았다면 재부팅을 다시하고나서 한다면 바뀌어져있을 것이다.

---------------------------------------------------------------------------------  
### 

- 젯슨나노에 usb카메라를 설치하고 데이터 케이블로 노트북과 젯슨나노를 연결해준다.  
- 그다음에 노트북에서 windows powershell을 열여준다.  
- 'ssh <username>@192.168.55.1'입력, 요청 시 설정한 암호를 입력합니다.  (여기서 <username>은 자신이 우분투를 설치할 때 썼던 이름을 입력)  
- 로그인한 젯슨 나노 터미널에서 'mkdir -p ~/nvdli-data'를 사용하여 활용될 데이터 디렉토리를 추가한다.  
  
- ls명령어는 디렉토리내 어떤 파일들이 있는지 보여줌
  
#### 다음 명령어를 통해 도커 컨테이너를 실행합니다. 여기서<tag>는 교육 과정 버전과 Jetson Nano JetPack L4T 운영 체제 버전의 조합입니다. (양식은 <tag> = <course_version>-<L4T_version>). 태그 목록은 NVIDIA NGC cloud page에서 확인하실 수 있습니다.  
     

- sudo docker run --runtime nvidia -it --rm --network host \    (docker는 컨테이너 이미지들이 저장되어 있는 docker저장소를 구축, 실행, 푸시를 하기위한 명령어)
- --volume ~/nvdli-data:/nvdli-nano/data \    (nvdli-data 디렉토리를 만들었던 것이 /nvdli-nano/data 디렉토리 안에 있고 volume이 하는 것은 이 두가지 디렉토리를 묶어 저장 공간을 공유하는 것이다. -> 그래서 /nvdli-nano/data 디렉토리에서 작업을 하다가 나가도 /nvdli-nano/data 디렉토리에 저장되어 있는 것이 nvdli-data 디렉토리 안에 유지되는 것이다.)
- --device /dev/video0 \     (디바이스 옵션은 usb를 통해 셋업을 할 것이기 때문에 video0)
-  nvcr.io/nvidia/dli/dli-nano-ai:<tag>
  
   
 - echo "sudo docker run --runtime nvidia -it --rm --network host \
    --volume ~/nvdli-data:/nvdli-nano/data \
    --device /dev/video0 \
    nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1kr" > docker_dli_run.sh    (재사용 가능한 스크립트를 만드는 것)
    chmod +x docker_dli_run.sh   (스크립트를 실행가능하게 만듦)
 -  ./docker_dli_run.sh   (스크립트를 실행,  앞으로는 이 명령문만 쓰면 들어갈 수 있음)  
     
 - 이후 웹브라우저에서 192.168.55.1:8888을 치게되면 주피터랩 서버가 열리게 되고 여기서'dlinano'라는 암호를 입력하면 로그인이 됨  
   
 --------------------------------------------------------------------------------------------------  
 ### 주피터 랩  
   
 ![7](https://user-images.githubusercontent.com/102521625/202904282-5d5a69d0-2455-4adc-b5ff-4d0793082f17.png)
  
   
 - tip 
   > - launcher 페이지에서 터미널을 열 수 있다. 여기서 'free -m'을 통해 스왑을 확인할 수 있다.  
   > - 만약 launcher가 없어졌을 경우, 사진에서처럼 +를 눌러서 launcher를 새로 열 수 있다.  
   > ![5](https://user-images.githubusercontent.com/102521625/202903598-8af0564e-4318-4e3f-8aba-46fb856fe60f.jpg)  
   > - data 디렉토리에 저장된 것은 종료 후에도 계속 유지되기 때문에 작업을 마친 데이터를 다시 수집할 필요없다.  
     
 - 실행하고 싶은 셀을 클릭 후, 삼각형 아이콘을 클릭하면 실행된다.  
   ![8](https://user-images.githubusercontent.com/102521625/202904311-b0e5c219-8ae1-4952-939c-8db7cdf631f9.png)
   그러면 셀의 옆에 숫자가 보이는데 그것은 실행되었다는 표시이다.  (tip : 빠르게 실행하고 싶다면 shift+enter를 누르면 조금 더 빨리 이동할 수 있다.)

   

