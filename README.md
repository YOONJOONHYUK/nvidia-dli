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
sudo echo "/mnt/4GB.swap swap swap defaults 0 0" >> /etc/fstab)


![4](https://user-images.githubusercontent.com/102521625/202901583-06260127-467e-4a9b-a759-f88843453c87.jpg)
- 위에와 같은 화면이 나오는데 여기서 사진에 있는 마지막 한줄을 쳐주게되면 스왑이 된 것이다.  
- 여기서 창을 닫기 위해서 ':wq'라는 명령어를 쳐서 닫고 다시 'free -m'을 쳐서 확인한다.  
- 하지만 여기서 아직도 용량이 변하지 않았다면 재부팅을 다시하고나서 한다면 바뀌어져있을 것이다.

  

