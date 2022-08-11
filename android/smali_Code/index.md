---
title: "smali code"
date: 2022-04-01T03:06:10+09:00
slug: android/smali_code
categories:
    - android
tags: [smali code]
---

## 타입
```
I – int
J – long
Z – Boolean
D – double
F – float
S – short 
C – char
V - void
```
## 메소드 종류
Static : this 인수가 암묵적으로 첫번째 인수로 전달되지 않으면, Static 메소드  
Direct : vtable 개입 없이 직접 invoke 함 (ex. private method, constructor)  
Virtual : 자식 클래스에서 override 될 수 있는 Virtual 메소드. 클래스 관련됨 vtable을 사용해 invoke 함  


### Register 간 데이터 이동
```
move
move/from16
move-wide
move-wide/from16
move-object
move-object/from16
```

### 리턴 세팅 및 처리
```
move-result
move-result-wide
move-result-object
return-void
return
return-wide
return-object
```
### 예외 처리
```
throw
move-exception
```
### 레지스터에 상수 대입
```
const/4
const
```
인스트럭션 패밀리
### 레지스터간 move
```
move, move/from16, move-wide, move-wide/from16, move-object, move-object/from16
```
### 결과값을 얻거나 세팅
```
move-result, move-result-wide, move-result-object, return-void, return,
return-wide, return-object
```
### 예외처리
```
throw, move-exception
```
### 레지스터에 상수 대입
```
const/4, const/16, const, const/high16, const-wide/1, const-wide/32,
const-wide, const-wide/high16, const-string, const-class
```
### 동기화
```
monitor-enter, monitor-exit
```
### 타입체크
```
check-cast, instance-of
```
### 배열 조작
```
new-array, array-length, filled-new-array, filled-new-array/range,
fill-array-data
```
### 인스턴스생성
```
new-instance
```
### 실행 조작
```
goto, goto/16, packed-switch, sparse-switch,
if-eq, if-ne, if-lt, if-ge, if-gt, if-le, if-eqz, if-nez, if-ltz, if-gez, if-gtz,
if-lez
```
### 비교
```
cmpl-float
cmpg-float
cmpl-double
cmpl-double
cmpg-double
cmp-long
```
### 멤버필드에 읽기/쓰기
```
iget
iget-wide
iget-object
iget-boolean
iget-byte
iget-char
iget-short
```
### 배열요소에 읽기/쓰기
```
aget
aget-wide
aget-object
aget-boolean
aget-byte
aget-char
aget-short
```
### 메소드 호출
```
invoke-virtua
invoke-super
invoke-direct
invoke-static
invoke-interface
invoke-virtual/range
invoke-super/range
invoke-direct/range
invoke-static/range
invoke-interface/range
```
### 연산 명령(int, long, float, double)
```
add
sub
mul
div
rem
```
## Smali snippet
### so 라이브러리 로드
```
const-string v0, "so_file_name"
invoke-static {v0}, Ljava/lang/System;->loadLibrary(Ljava/lang/String;)V
```
### 로그 출력
```
.local v0, "Log":Ljava/lang/String;
const-string v1,  "hack" //출력할 문자열 혹은 레지스터
invoke-static {v1, v0}, Landroid/util/Log;->e(Ljava/lang/String;Ljava/lang/String;)I
```
### sleep
```
const-wide/16 v2, 0xa  // 0xa = 10
invoke-static {v2, v3}, Ljava/lang/Thread;->sleep(J)V
```

### toast 출력
```
const-string v0, "Toast TEST"
const/4 v1, 0x0
invoke-static {p0, v0, v1}, Landroid/widget/Toast;->makeText(Landroid/content/Context;Ljava/lang/CharSequence;I)Landroid/widget/Toast;
move-result-object v0
invoke-virtual {v0}, Landroid/widget/Toast;->show()V
```
