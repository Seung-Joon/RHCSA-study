# Part4 Selinux 설정.
사실..RHCSA수준에서는 아주 간단한 수준의 SELINUX 설정 Skill만 요구한다.  
간단한 내용만 다루겠다.  

## 1. 셀리눅스?
  - 어느 프로세스가 어느 파일, 디렉터리, 포트에 액세스 할 수 있는지 결정하는 **보안 규칙의 집합.**
  - SELINUX 에 해당 규칙이 없을경우 액세스가 허용되지 않는다.
  - SELINUX의 모드는 총 3가지로 다음과 같다.
    * enforcing   # 보안 활성화
    * permissive  # 보안 비활성화 및 보안 기록 로깅
    * disable     # 비활성화

## 2. SELINUX 모드 설정
```bash
[root@station]# vim /etc/selinux/config

# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=enforcing # 이부분이 모드를 지정하는 부분이다. (철자 및 오타에 주의하며 입력할것. 잘못입력하면 부팅 안됨)
# SELINUXTYPE= can take one of three values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected. 
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted

[root@station]# getenforce  # 셀리눅스 설정상태 확인법
Enforcing
```
 