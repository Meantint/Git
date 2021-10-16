# Git

## Git이 필요한 이유

1. 버전 관리(Version Control)

   - Git은 문서를 수정할 때 언제 수정했는지, 어떤 것을 변경했는지 편하고 구체적으로 기록할 수 있다.

2. 백업(Backup)

   - 자료를 하나의 공간에 저장한다면 시간이 지날수록 자료가 유실될 확률이 증가한다. 이러한 불확실성을 제거하기 위해서 백업을 해줘야한다.

   - Git 파일 백업을 위한 원격(온라인) 저장소들이 존재한다. 대표적으로 Github, Gitlab 등이 있다.

3. 협업(Collaboration)

   - Github와 같은 원격 저장소를 이용하면 여러 사람이 함께 협업할 수 있는 장점이 생긴다.

   - 어떤 부분이 생성, 수정, 제거 되었는지를 기록할 수 있기 때문에 오류가 생겨도 파악하기가 쉽다.

## 내 환경

Ubuntu 20.04.3 LTS

WSL2

## 설치

```bash
sudo apt-get install git
# 제대로 설치가 됐다면 git 명령어를 쳤을 때 여러 옵션들이 나타난다.
git
```

## Git 환경 설정

Git 사용 전에 사용자 정보를 입력해줘야한다. Git은 버전을 저장할 때 마다 사용자 정보도 함께 저장하기 때문이다.

```git
# user.name 뒤에 이름을 넣는다.
git config --global user.name "user_name"

# user.email 뒤에 이메일을 넣는다.
git config --global user.email "user_email"
```

위 명령어의 `--global` 옵션은 현재 컴퓨터의 모든 저장소에서 같은 사용자 정보를 사용하도록 설정해주는 명령어이다.

## 참고

- [지옥에서 온 문서 관리자 깃&깃허브 입문](https://opentutorials.org/course/2708)

- [https://git-scm.com/book/ko/v2](https://git-scm.com/book/ko/v2)