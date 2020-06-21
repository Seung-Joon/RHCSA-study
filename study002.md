# Part2 호스트 네임과, 네트워크 <사전작업>
## 호스트 이름과 네트워크를 다음과 같이 설정하십시오.
```
Host Name: station.domain11.example.com
IP/Netmask: 172.24.11.10/24
Default route: 172.24.11.254
dns: 172.24.11.250
```
## yum repository 를 다음과 같이 설정하십시오.
```
Base Url: http://download.fedoraproject.org/pub/epel/7/x86_64/
```

## 1. 호스트네임 설정하기
``` bash
[root@station]# hostnamectl set-hostname station.domain11.example.com
[root@station]# hostname #설정내용 확인
```

## 2. 네트워크 설정하기
- GUI로 설정하기 (eth0)
```bash
[root@station]# nmtui # 아이피 설정
[root@station]# nmcli connection up eth0 # eth0 에 변경사항 적용
[root@station]# ifconfig # 변경사항 확인
```
- 참고사항
```bash
# 이때 디바이스를 찾지 못하는경우가 있다. 
# 아래의 방법은 eth0 장치의 UUID를 확인하여 변경사항을 적용하는 방법이다.
[root@station]# nmcli con show
NAME         UUID                                  TYPE      DEVICE 
System eth0  a0e144c4-b5ef-4c09-8f92-d3448e6d2196  ethernet  eth0   
virbr0       8e812d0a-1f4e-4652-a5f0-5b57e5cb83d0  bridge    virbr0 

[root@station]# nmcli connection up a0e144c4-b5ef-4c09-8f92-d3448e6d2196
[root@station]# ifconfig # 변경사항 확인
```

## 3. 레포지토리 설정하기
- 터미널
  ```bash
  [root@station]# vim /etc/yum.repos.d/(생성할 파일 이름).repo
  ```
- 편집기
  ```bash
  [(생성한 이름)]
  name=server
  baseurl=(레포지토리 주소)
  enabled=1
  gpgchk=0

  # 경우에 따라 gpg를 체크할 수 있다.
  # gpg를 체크하는 요구사항이 있을경우 아래와 같이 설정한다.
  # gpgchk=1
  # gpgchk=example.com
  ```
- 터미널
  ```bash
  [root@station]# yum clean all
  [root@station]# yum update
  [root@station]# yum repolist # 레포지토리 확인.
  ```

