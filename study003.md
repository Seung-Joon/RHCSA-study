# Part3 GUI, CLI 환경

## 1. System RunLevel List
    0: halt # 시스템 중지  
    1: single user # 시스템 복원 모드  
    2: multiuser mode  # without nfs(네트워크 사용 안함)  
    3: **Full-multiuser** # 일반적인 쉘 기반 다중 사용자 모드  
    4: None  
    5: **Graphic User Mode**   
    6: reboot  

## 2. GUI 환경 설치 
```bash
[root@station]# yum group install "GNOME Desktop" -y
[root@station]# ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target #소프트링크 생성
```
## 3. GUI <-> CLI 환경전환

```bash
[root@station]# systemctl isolate multi-user.target # GUI -> CLI 전환
[root@station]# systemctl isolate graphics.target   # CLI -> GUI 전환 

[root@station]# systemctl set-default xxx.target # 부팅 기본모드 설정. 
```