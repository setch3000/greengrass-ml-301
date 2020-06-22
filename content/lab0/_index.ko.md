---
title: 실습 1. CloudFormation을 활용한 AWS Resource 생성 (25분)
weight: 20
pre: "<b>1. </b>"
---

### CloudFormation을 활용한 AWS Resource 생성

이 워크샵에 필요한 AWS 리소스를 생성하기 위해 CloudFormation 스택을 제공합니다.\
CloudFormation 스택은 AWS Greengrass를 실행하는 데 사용될 EC2 인스턴스를 다른 리소스 중에서 생성합니다. 또한 SageMaker 노트북 인스턴스가 생성되고 부트 스트랩됩니다.\
아래 링크를 선택하면 스택이 시작될 AWS 콘솔의 CloudFormation 으로 자동 redirection됩니다.

* [Launch CloudFormation stack in us-east-1 (N. Virginia)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?stackName=PublicIoTWorkshop&templateURL=https://public-cloudformation.s3.ap-northeast-2.amazonaws.com/greengrass-ml-301/greengrass-ml-301.yml)


CloudFormation 스택은 최소한 다음 리소스를 만듭니다.

* SageMaker에 필요한 S3 버킷
* EC2 및 SageMaker 인스턴스에 퍼블릭 서브넷 + 보안 그룹이있는 VPC
* Greengrass를 실행하고 Lambda 함수를 생성하는 Cloud9 인스턴스
* Jupyter 노트북에서 모델을 정의하는 SageMaker 노트북 인스턴스. 모델 자체는 AWS SageMaker 서비스를 사용하여 학습됩니다.
* Cloud9 인스턴스의 인스턴스 프로파일
* 사물(thing)의 역할을 하는 EC2 instance - 본 워크샾에서는 EC2를 IoT의 사물(thing)으로써 사용합니다.
* AWS 리소스에 액세스하는 데 필요한 IAM 역할

AWS CloudFormation 콘솔의 Quick create stack 페이지로 리디렉션 된 후 다음 단계를 수행하여 스택을 시작하십시오.

* EC2 Instance에 SSH로 접근하기 위한 kaypair를 지정합니다.
* Capabilities 에서 ***I acknowledge that AWS CloudFormation might create IAM resources***을을 체크합니다.
* Create stack 버튼을 누르고, stack 생성이 완료될 때까지 기다립니다. 10분 정도 소요됩니다.

![picture1.png](images/picture1.png)

CloudFormation 콘솔의 스택에 대한 ***Output*** 섹션에서 생성 된 리소스에 대한 정보르 찾을 수 있습니다. 언제든지 ***Output*** 섹션으로 돌아와서 값을 확인할 수 있습니다.

![picture2.png](images/picture2.png)

#### Cloud9 IDE에 접속

생성하신 CloudFormation 스택에서 ***Output*** 섹션을 확인합니다.
Cloud9IDE 항목의 링크에서 오른쪽 마우스를 클릭하여 ***Open link in new tab***선택합니다.

![picture3.png](images/picture3.png)

하기 화면과 같은 Cloud9 instance로 이동됩니다.
아래 명령으로 남은 저장 공간을 확인할 수 있습니다.

``` shell
df -h
```

![picture-df.png](images/picture-df.png)


#### home folder가 보여지도록 설정

Workshop에서 사용되는 많은 파일이 Cloud9 IDE에 복사되어 있습니다. 기본적으로 홈 폴더의 내용은 표시되지 않습니다. 따라서 이것을 변경해야합니다.

![picture-home.png](images/picture-home.png)

#### Open a Terminal

Cloud9 IDE에서 terminal (shell)을 열기 위해서 Tab bar에서 ***+***를 클릭하고 ***New Terminal***을 선택합니다.

![picture-new.png](images/picture-new.png)


#### EC2에 SSH로 연결하기 위한 keypair 파일 업로드

본 워크샾에서는 EC2를 IoT의 사물(thing)으로써 사용합니다. 사물(thing)의 역할을 하는 EC2에 접속하기 위하여 keypair 파일을 Cloud9에 업로드합니다.

먼저 FILE SYSTEM에서 /home/ec2-user/environment 폴더를 클릭한 상태에서

![picture5.png](images/picture5.png)

상단의 메뉴에서 File > Upload Local Files... 를 선택하여 EC2에 접속하기 위하여 keypair 파일을 Cloud9에 업로드합니다. 여기에 업로드하는 파일은 조금 전 CloudFormation에 명시했던 keypair 파일과 동일한 것이어야 합니다.

![picture6.png](images/picture6.png)

keypair 파일이 업로드되면 아래와 같이 보여집니다.

![picture7.png](images/picture7.png)

keypair 파일이 업로드되면 아래와 같은 명령으로 permission을 변경해 줍니다.

``` shell
chmod 400 <키페어 파일 이름>
```

아래는 예제입니다.

``` shell
chmod 400 ee-default-keypair.pem 
```

수고하셨습니다. 실습 1을 완료하셨습니다.
