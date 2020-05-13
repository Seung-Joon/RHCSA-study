# Part2 호스트 네임과, 네트워크 <사전작업>
## 호스트 이름과 네트워크를 다음과 같이 설정하십시오.
```
Host Name: station.domain11.example.com
IP/Netmask: 172.24.11.10/24
Default route: 172.24.11.254
dns: 172.24.11.250
```
## yum repository 설정하기
```
Base Url: http://nginx.org/packages/centos/7/$basearch/
```


## 1. 네트워크 설정하기
- GUI로 설정하기
```
nmtui # 아이피 설정
nmcli connection up (target) # 변경사항 적용
ip addr # 변경사항 확인
```

## 2. 호스트네임 설정하기
```
hostnamectl set-hostname (설정할 호스트네임)
hostname #설정내용 확인
```

## 3. 레포지토리 설정하기
- 터미널
  ```git 
  vi /etc/yum.repos.d/(생성할 파일 이름).repo
  ```
- 편집기
  ```
  [(생성한 이름)]
  name=server
  baseurl=(레포지토리 주소)
  enabled=1
  gpgchk=0
  ```
- 터미널
  ```
  yum clean all
  yum repolist
  ```

