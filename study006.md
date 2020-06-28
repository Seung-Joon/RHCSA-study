# Part6 SWAP 영역

## 목표
  >  - /dev/sdb에서 300M 크기의 SWAP 파티션을 할당하십시오.
  >  - 생성한 메모리의 우선순위를 1 로 설정하십시오.
  >  메모리는 재부팅 이후에도 마운트가 유지되어야 합니다.

## SWAP 영역이란??
  - 디스크의 일부를 메모리로 사용할 수 있도록 하는 가상 메모리 기술.
  - 메모리에 적재되어 있으나 사용하지 않는 프로세스를 해당 메모리로 이동하여 RAM의 가용영역을 확대하는 목적임.
  - SWAP 영역에 적재된 프로세스를 다시 사용하는 경우 RAM에 다시 적재함.

## 1. 파티션 생성
  ```bash
  [root@station]# fdisk /dev/sdb
    > n            # 파티션 생성
    > p            # 프라이머리로 생성
    > 2            # 1번 파티션 선택
    > [enter].       # 사용가능한 실린더부터
    > +300M       # 300M 만큼 실린더를 설정한다.
    > t             # 파티션 타입 지정
    > 1            # 1번 파티션 선택
    > 82           # swap용 타입 지정 (l 로 확인 후 지정할것.)
    > w            # 저장
  ```

# 2. SWAP 생성
  ```bash
  [root@station]# mkswap /dev/sdb2 # SWAP 영역 생성.
  [root@station]# swapon /dev/sdb2 # SWAP 영역 활성화.
  ```

# 3. 자동 마운트 설정
  ```bash
  [root@station]# $ blkid /dev/sdb2    # UUID 확인 
  [root@station]# vim /etc/fstab
   UUID=[확인한장치uuid].   swap   swap   pri=1    0   0

  [root@station]# $ swapon /dev/sdb2
  [root@station]# $ reboot
  [root@station]# $ swapon -s # swap 메모리 확인
  ```