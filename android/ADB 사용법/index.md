---
title: "ADB 사용법"
date: 2022-04-01T08:43:09+09:00
slug: android/ADB 사용법
categories: 
    - Android
---

## 1. ADB

 ADB 사용하기

[https://forum.xda-developers.com/t/tool-minimal-adb-and-fastboot-2-9-18.2317790/](https://forum.xda-developers.com/t/tool-minimal-adb-and-fastboot-2-9-18.2317790/)

adb shell  
adb devices 
<br></br>
옵션   
-e : 에뮬레이터   
    -d : USB 장치  
    -s : adb -s <장치명> <명령어>   
- - -

설치치된 패키지 찾기

```
>adb shell pm list packages | find "<패키지 이름이나 키워드>"
```

apk의 정확한 패키지 이름 확인 후, apk 설치 위치를 확인합니다.

```
>adb shell dumpsys package <패키지 이름> | find "path"
```

### **adb 기본 명령어(?)**

```jsx
adb devices
adb connect 127.0.0.1:62001
adb shell
```

### **로그 분석**

```c
adb logcat  : 안드로이드 장치에서 발생하는 로그메시지 출력

adb logcat --pid=<pid> : 특정 프로세스 로그만 출력

```

### **프로세스 목록 확인**

```powershell
adb jdwp

// 해당 어플 실행전 adb jdwp 결과값과 실행후 결과값을 비교하여 추가된 PID로 분석
```

### **어플리케이션 제어**

```powershell
**// 어플리케이션 설치**
adb install <apk_파일>

**// 동일한 어플리케이션 설치되어있을경우 기존데이터 삭제 없이 설치**
adb -r install <apk_파일> | grep <설치된 어플리케이션>

**//설치된 어플리케이션 패키지 목록**
adb shell pm list packages -f 

**// 어플리케이션 삭제**
adb uninstall <설치된패키지명>
```

### **파일제어**

```powershell
**// 에뮬레이터/장치 → PC로 파일 복사**
adb pull <장치 경로> <pc저장 위치>

**// PC -> 에뮬레이터/장치로 파일 복사**
adb push <pc파일위치> <장치저장 위치>
```

### **포트와 네트워킹**

```powershell
**// 로컬 포트를 안드로이드 장치의 특정 포트와 소켓 통신**
adb forward <로컬> <원격지> 
adb forwoard tcp:7777 tcp:8888

**// 디버깅**
adb forwoard tcp:7777 jdwp:1824
jdb -sourcepath <경로> -connect 
```

### **스크립팅**

```powershell
**// 장치 시리얼 번호 출력**
adb get-serialno

**// 장치 상태 문자열로 출력**
adb get-state

**// 장치 구동시 명령어 실행**
adb wait-for-device <명령어>
```

### **서버**

```powershell
**// ADB 서버 프로세스 동작여부 확인후 결과 표시, 동작중이지 않으면 서버 구동시킴**
adb start-server

**// 서버종료**
adb kill-server
```

### **버그 보고서**

```c
adb bugreport
```