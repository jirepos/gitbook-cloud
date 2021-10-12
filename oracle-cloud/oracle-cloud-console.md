# Oracle Cloud Console 설정

무료로 서버를 운영할 클라우드 서비스를 찾다가 오라클 클라우드가 무료로 운영할 수 있다고 하여 등록했다. 신용카드 정보가 필요하여 입력을 하였다. 업그레이드를 요청하지 않으면 무료라고 한다.

등록을 하면 다음과 같은 화면이 나온다.

![](<../.gitbook/assets/image (63).png>)



[Oracle Cloud Console](https://cloud.oracle.com)

## VM 인스턴스 생성

서버를 만들어야 하니까 'VM 인스턴스 생성'을 클릭한다. 컴퓨트 인스턴스 생성 화면이 표시된다.

먼저 인스턴스의 이름을 입력한다.

![](<../.gitbook/assets/image (43).png>)



OS를 직접 선택할 수 있다. '편집' 링크를 클릭한다.

![](<../.gitbook/assets/image (5).png>)



우분투를 선택해 보자. 맨 아래에 '이미지 선택' 버튼을 클릭한다.

![](<../.gitbook/assets/image (7).png>)



이미지 및 구성이 다음과 같이 화면이 변경된다.

![](<../.gitbook/assets/image (29).png>)





공개키 생성은 Putty Key Generator를 사용한다. 공개키를 등록한다.

> 처음 인스턴스를 생성할 때 이것을 안해서 그런지 ssh로 접속이 불가능했다. Putty Key Generator를 사용하기고 하고 git의 ssh-keygen을 사용해 보았는데 접속이 불가능했다. 아마도 이 시점에서 먼저 ssh 키를 등록해야 하는 것 같기도 하다. 그래서 인스턴스를 재생성하려고 '종료'를 실행했는데 다른 인스턴스를 만들 수는 없었다. 검색해보니 24시간이 지나야 한다고 하는데........ 24시간이 지나봐야 알 것 같다.

> 24시간이 지났다. 다시 인스턴스를 만들려고 시도했다. 여전히 용량이 부족하다는 메시지가 나오면서 인스턴스를 만들 수 없었다. 분명히 인스턴스 목록에는 없었는데 말이다. 어제 인스턴스 다시 생성하면서 혹시 안되는 이유가 Ubuntu라서 안되는 것 같아서 디폴트인 Oracle Linux를 선택해서 계속 시도를 했었고 오늘도 동일한 Oracle Linux로 시도를 했었다.

> 오라클을 검색해보니 Oracle Linux가 아닌 Ubuntu로 설정하고 인스턴스를 생성하라고 해서 Ubuntu로 생성하니 생성이 되었다. 이번에 생성할 때에는 Putty Key Gen으로 생성한 공개키를 복사해 붙여넣었다. 그리고 Putty로 접속하니 접속이 되었다. 이 순서에서 공개키 복사하는 것을 잊지 말아야 한다.



![](<../.gitbook/assets/image (15).png>)

나머지 설정은 무시하고 맨 아래의 '생성' 버튼을 클릭한다. 인스턴스 생성 결과가 화면에 표시된다.



![](<../.gitbook/assets/image (13).png>)



VM에 접근할 수 있는 네트워크 정보도 표시된다.

![](<../.gitbook/assets/image (61).png>)



## 블록 볼륨 리소스 생성

블록 볼륨은 부트 볼륨과 별개의 네트워크 하드 드라이브를 생성하고 VM의 파일 시스템에서 이를 마운트 한다. 블록 볼륨은 부트 볼륨과 별개이다.

**세 단계 설정**

* 오라클 클라우드 콘솔에서 블록 볼륨 리소스 생성
* 블록 볼륨을 VM 인스턴스에 연결
* VM 인스턴스에서 블록 볼륨을 파일 시스템으로 마운트

### 블록 볼륨 생성

'스토리지>블록 볼륨' 선택한다.



![](<../.gitbook/assets/image (41).png>)

'블록 볼륨 생성' 버튼을 클릭한다.



![](<../.gitbook/assets/image (21).png>)



볼륨이름을 설정한다. 나머지는 다 디폴트로 놓고 맨 아래에 '블록 볼륨 생성' 버튼을 클릭한다.

### 블록 볼륨 VM 인스턴스에 연결

블럭 볼륨 생성과 마찬가지로 '스토리지>블록 볼륨' 선택한다. 생성된 블럭 볼륨이 보일 것이다. 여기서 생성된 블럭 볼륨을 클릭한다.



![](<../.gitbook/assets/image (1).png>)

왼쪽 하단에 '연결된 인스턴스' 링크가 보일 것이다. 클릭한다. 



![](<../.gitbook/assets/image (14).png>)





'인스턴스에 연결' 버튼을 클릭한다. 

![](<../.gitbook/assets/image (54).png>)



옵션을 선택한다.

* 연결 유형 : ISCSI
* 엑세스 유형: 읽기/쓰기

인스턴스를 선택하고 장치경로를 선택한다. 



![](<../.gitbook/assets/image (60).png>)



맨 아래의 '연결' 버튼을 클릭한다. '연결 중'이라고 나온다. 좀 기다려야 한다. 다 연결되면 '연결됨'으로 표시된다.

인결된 인스턴스 링크의 오른쪽에 '생성' 열이 있다. 여기서 더보기 매뉴를 클릭하여 'ISCSI 명령 및 정보'를 클릭한다.

![](<../.gitbook/assets/image (28).png>)





'iSCSI 명령 및 정보' 화면이 표시되는데 명령어들을 복사한다.

![](<../.gitbook/assets/image (16).png>)





**접속용 명령**

```shell
sudo iscsiadm -m node -o new -T iqn.2015-12.com.oracleiaas:6326b5da-c7d8-4419-a993-29d8d8d63285 -p 169.254.2.2:3260
sudo iscsiadm -m node -o update -T iqn.2015-12.com.oracleiaas:6326b5da-c7d8-4419-a993-29d8d8d63285 -n node.startup -v automatic
sudo iscsiadm -m node -T iqn.2015-12.com.oracleiaas:6326b5da-c7d8-4419-a993-29d8d8d63285 -p 169.254.2.2:3260 -l
```

**접속 해제용 명령**

```shell
sudo iscsiadm -m node -T iqn.2015-12.com.oracleiaas:6326b5da-c7d8-4419-a993-29d8d8d63285 -p 169.254.2.2:3260 -u
sudo iscsiadm -m node -o delete -T iqn.2015-12.com.oracleiaas:6326b5da-c7d8-4419-a993-29d8d8d63285 -p 169.254.2.2:3260
```

접속용 명령을 모두 실행하고 lsblk 명령어로 블록볼륨이 마운트 되었는지 확인한다.

```shell
lsblk
```

마지막 줄에 sdb가 마운트 된 것을 확인할 수 있다.

```shell
ubuntu@instance-20210604-1640:/$ lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0     7:0    0 55.5M  1 loop /snap/core18/1997
loop1     7:1    0 79.2M  1 loop /snap/oracle-cloud-agent/17
loop2     7:2    0 32.1M  1 loop /snap/snapd/11841
sda       8:0    0 46.6G  0 disk
├─sda1    8:1    0 46.5G  0 part /
├─sda14   8:14   0    4M  0 part
└─sda15   8:15   0  106M  0 part /boot/efi
sdb       8:16   0   50G  0 disk
ubuntu@instance-20210604-1640:/$
```

### VM 인스턴스에서 블록 볼륨을 마운트

마운트 한 블록 볼륨을 ext4로 포맷한다.

```shell
sudo mkfs.ext4 -m 0 -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb
```

다음과 같이 포맷이 완료된다.

```shell
ubuntu@instance-20210604-1640:/$ sudo mkfs.ext4 -m 0 -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 13107200 4k blocks and 3276800 inodes
Filesystem UUID: 8cf8f256-8223-4f88-9065-a30dd2416207
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
        4096000, 7962624, 11239424

Allocating group tables: done
Writing inode tables: done
Creating journal (65536 blocks): done
Writing superblocks and filesystem accounting information: done
```

Symlink 연결한다.

```shell
sudo mkdir -p /mnt/disks/sdb
sudo mount -o discard,defaults /dev/sdb /mnt/disks/sdb
sudo chmod a+w /mnt/disks/sdb
```

/etc/fstab 작성을 위한 HDD의 UUID 확인

```shell
sudo blkid /dev/sdb
```

```shell
ubuntu@instance-20210604-1640:/$ sudo blkid /dev/sdb
/dev/sdb: UUID="999999-9999-9999-9999-9999999999999" TYPE="ext4"
```

/etc/fstab을 vi로 열어 편집한다. 주의해야 할 점은 블록 볼륨이 네트워크 드라이브이기 때문에 \_netdev 옵션을 사용해야 한다. UUID=UUID_VALUE /mnt/disks/sdb ext4 discard,defaults,nobootwait 0 2\* \_netdev

```
UUID="999999-9999-9999-9999-9999999999999" /mnt/disks/sdb ext4 discard,defaults,noatime,_netdev 0 2
```

> vi가 없으면 'apt-get update' 실행

그런데 권한이 없다고.

오라클 클라우드 우분투에서 ROOT 계정으로 접속하려면

root 계정에 비밀번호 생성 및 로그인해야 한다.

우선 맨 처음 필요한 것은 root 계정에 Password를 만들어 준다.

명령창에 sudo passwd root 를 입력한다.

그리고 다시 apt-get update

그래도 vi가 없다.

root 로그인 해제 및 비밀번호 인증 변경한다. 명령창에서 다음을 입력

```shell
nano /etc/ssh/sshd_config
```

[여기 참조](https://itreport.tistory.com/638) 이거 남은 작업 있음.

vi를 설치한다.

```
sudo apt-get install vim 
```

이제 정상적으로 vi를 쓸 수 있다.

mount한다.

```shell
sudo mount -all
```

mount -all 한 결과를 확인하기 위해서 df명령어로 /mnt/disks/sdb 에 마운트 여부를 확인한다.

```shell
df -h
```

이제 마운트된 위치로 들어가보자.

```
cd /mnt/disks/sdb
```
