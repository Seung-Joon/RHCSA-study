# Part 1 - Break Root Password <사전작업>

## Root 계정의 비밀번호를 redhat 변경하십시오. 
1. Botting 화면 -> 맨 위 커널버전에서 "e" 를 입력한다.
2. linux16~~~~ 으로 시작하는 line 끝에 한칸 뛴 후 rd.break를 입력한다.
3. ctrl + x 를 눌러 switch로 시작하는 프롬프트로 전환한다.
4. 지금부터 명령어 입력.
   ```
   switch_root:/#  mount -o remount,rw /sysroot
   switch_root:/#  chroot /sysroot
   sh-4.2# passwd root #비밀번호 입력
   sh-4.2# touch /.autorelabel #부팅 후 시스템이 SELINUX가 relabel을 실행하도록 설정
   sh-4.2# exit
   exit
   switch_root:/# exit
   logout
   ```
   
   #### 여기까지 문제 없이 커맨드를 수행하였고 정상적으로 부팅이 된다면 로그인을 해보자.
   ```
   localhost login: root
   Password: redhat
   ```

   ## 로그인이 되었다면 성공이다.
