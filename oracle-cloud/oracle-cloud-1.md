# Oracle Cloud 머신러닝 샌드박스 구축

인스턴스에 소프트웨어를 설치하기 전에 로컬 컴퓨터에서 인터넷을 통한 트래픽을 허용하도록 구성해야 한다. 액세스 권한을 설정한 후 Anaconda를 설치한 다음 사용할 머신 러닝 환경을 생성한다.

## Oracle Cloud Infrastructure Compute 인스턴스 설정

상태 유지 규칙을 사용하는 것이 가장 쉽다. 본질적으로 stateful 규칙은 선택된 포트에서 수신 및 응답 모두 허용한다. Stateless 수신 규칙을 설정하는 경우 해당 송신 규칙도 설정해야 한다.

* 기본적으로 포트 8888을 사용하는 Jupyter Notebook에 대한 ingress 규칙을 추가합니다.
  * Oracle Cloud 콘솔에 로그인하고 탐색 메뉴를 엽니다.
  * 네트워킹으로 이동하여 가상 클라우드 네트워크 를 누릅니다.
  * 관심 있는 클라우드 네트워크를 누릅니다.
  * 리소스 아래에서 보안 목록 을 누른 다음 관심 있는 보안 목록을 누릅니다.
  * 리소스 에서 수신 규칙 을 누르고 수신 규칙 추가 를 누릅니다.
  * 소스 CIDR의 경우 0.0.0.0/0 , IP 프로토콜의 경우 TCP , 대상 포트 범위의 경우 8888을 입력합니다.
  * 수신 규칙 추가 를 누릅니다.
* 방화벽 규칙을 업데이트합니다. 여기에 표시되는 명령은 Jupyter Notebook의 기본 포트인 포트 8888을 엽니다.

Ubuntu 에서 다음을 수행합니다.

```shell
sudo iptables -I INPUT -p tcp -s 0.0.0.0/0 --dport 8888 -j ACCEPT
sudo service netfilter-persistent save
```

## 분석 분포 설치

Anaconda 및 해당 패키지 관리자를 사용하여 컴퓨트 인스턴스에 개별 시스템 학습 환경을 설정하고 유지 관리합니다.

https://repo.continuum.io/archive/에서 최신 설치 프로그램을 가져올 수 있습니다. 이러한 지침은 운영 체제가 Oracle Linux 7 . 7또는 Ubuntu 18 . 04이고 Anaconda 배포의 버전이 Python 3 . 7의 2019.10이라고 가정합니다.

1. SSH 또는 PuTTY 를 사용하여 컴퓨트 인스턴스에 접속합니다.
2. Anaconda3 를 다운로드하고 체크섬이 https://repo.continuum.io/archive/. 에서 Anaconda 설치 프로그램 아카이브 페이지에 게시된 체크섬과 일치하는지 확인하십시오.

```shell
wget https://repo.continuum.io/archive/Anaconda3-2019.10-Linux-x86_64.sh

md5sum Anaconda3-2019.10-Linux-x86_64.sh
```

1. 설치 스크립트를 실행한 다음 경로에 분석 을 추가합니다.

```shell
bash Anaconda3-2019.10-Linux-x86_64.sh -b
echo -e 'export PATH="$HOME/anaconda3/bin:$PATH"' >> $HOME/.bashrc
source ~/.bashrc
```

1. 최신 conda가 있는지 확인합니다.

```shell
conda update -n base -c defaults conda
```

1. conda activate 명령을 사용하도록 셸을 구성합니다.

```shell
conda init bash
source ~/.bashrc
```

셸이 구성되면 현재 Anaconda 환경이 명령행 프롬프트에 추가됩니다. 기본 환경이 활성화되면 운영 체제에 따라 명령행이 다음 예제 중 하나와 유사해야 합니다.

```shell
(base) [opc@instancename ~]$
(base) [ubuntu@instancename ~]$
```

[참고](https://docs.oracle.com/ko/solutions/machine-learning-sandbox/configuring-your-system1.html#GUID-1B72D0BE-4C78-4624-B5DD-DC1479E4AC80)
