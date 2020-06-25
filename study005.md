# Part5 파일 시스템 마운트

## 목표
  >  - /dev/sdb에서 300M 크기의 파일 시스템을 할당하십시오.
  >  - 할당된 파티션은 xfs 형식으로 포맷되어야 합니다.
  >  - /mnt/point 에 마운트 되도록 설정되어야 하며 재부팅시 마운트가 유지되어야 합니다.

## 1. 파티션 할당 
  ```bash
  [root@station]# fdisk /dev/sdb
   > n    # 파티션 생성
   > p    # 프라이머리로 생성
   > [enter].       # 사용가능한 실린더부터
   > +300M       # 300M 만큼 실린더를 설정한다.
   > w           # 변경 내용을 저장한다. 
                 # tip: fdisk 명령은 실행 즉시 적용되는것이 아닌 버퍼에 명령어를 적재한 후 w 커맨드를 통해 명렁어를 실행하여 실제 시스템에 적용한다.
   
  [root@station]# fdisk -l /dev/sdb #  생성정보 확인
  ```

## 2. 파일 시스탬 생성
  ```bash
  [root@station]# mkfs -t ext4 /dev/sdb1
  ```

## 3. 파티션 마운트 
  ```bash
  [root@station]# blkid /dev/sdb1  # 장치 UUID 확인
  [root@station]# mkdir /mnt/point
  [root@station]# vim /etc/fstab
  UUID=[확인한장치uuid] /mnt/point.   ext4   default    1   2

  [root@station]# mount -a # 모든 내용에 대한 마운트 적용
  [root@station]# mount | grep fstab    # 마운트 확인

  [root@station]# reboot    # 재부팅
  [root@station]# mount | grep fstab    # 마운트 확인
  ```