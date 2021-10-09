# Git 기초(버전 관리)

## Git 초기화

Git 관리를 하고 싶은 폴더에서 다음의 명령어를 입력하자.

```bash
git init
```

`Initialized empty Git repository ...`라는 명령어가 나온다면 제대로 초기화가 완료된 것이다.

```bash
# 폴더를 확인하면 .git 폴더가 생성됐음을 알 수 있다.
ls -al
```

## Git 구조

Git의 구조는 다음 3개로 구성되어 있다.

### 작업 트리(Working Tree)

- 파일 수정, 저장 등의 작업을 하는 디렉터리. 우리 눈에 보이는 디렉터리이다.

### 스테이지(Stage)

- 버전으로 만들 파일이 대기하는 곳

- 눈에 보이지 않는다(.git 안에 숨김 파일로 존재)

### 저장소(Repository)

- 스테이지에서 대기하고 있던 파일들을 버전으로 만들어 저장하는 곳.

- 눈에 보이지 않는다(.git 안에 숨김 파일로 존재)

## Git이 버전을 만드는 과정

1. (생성, 수정, 제거) 중 하나를 작업한 파일이 작업 트리에 있다.

2. 작업 트리에 있는 파일 중 버전으로 만들고 싶은 파일을 스테이지에 넣는다.

3. 커밋(commit) 명령을 통해 스테이지에 대기하던 파일들을 모두 저장소로 옮기면서 새로운 버전이 생성된다.

## Git 상태(git status)

새로운 폴더를 만들고 그 안에서 `git init`을 통해 초기화 해보자. 이후 아무 작업 없이 `git status` 명령어를 통해 현재 깃의 상태를 확인해보자.

```bash
git status

# status message
On branch master
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```

- `On branch master` : 현재 `master` 브랜치에 있다는 의미

- `No commits yet` : 아직 커밋한 파일이 없다는 의미

- `nothing to commit` : 현재 커밋할 파일이 없다는 의미

이번에는 폴더에 임의의 파일을 만들고 저장한 후 `git status`를 입력해보자.

```bash
git status

# status message
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test.txt
```

- `untracked files` : 아직 한번도 버전 관리하지 않은 파일

현재의 `test.txt` 파일은 [Git이 버전을 만드는 과정](#git이-버전을-만드는-과정) 1번 상태이다.

## 수정한 파일 스테이징 하기(git add)

작업 트리 파일 중 원하는 파일들을 스테이지에 추가해준다.

스테이징(Staging)은 Git에게 버전 만들 준비를 하라고 알려주는 것이다. 스테이징에 사용하는 명령어는 `git add`이다.

```bash
git add test.txt # Staging test.txt
```

```bash
git status

# status message
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   test.txt
```

- `Changes to be committed` : 커밋할 변경 사항

- `new file` : 새 파일인 경우의 수식어

## 스테이지에 올라온 파일 커밋하기(git commit)

스테이지에 파일이 있다면 버전을 만들 수가 있다. Git에서는 버전 만드는 것을 커밋한다고도 말한다. 버전마다 어떤 변경사항이 있는지 메시지를 기록할 수 있다(해야 한다).

```bash
git commit -m "Create test.txt"

# commit message
[master (root-commit) fe2dc0f] Create test.txt
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test.txt
```

```bash
git status

# status message
On branch master
nothing to commit, working tree clean # 버전으로 만들 파일 X, 작업 트리도 수정사항 없다.
```

## 저장소 버전 확인하기(git log)

`git log` 명령어를 통해 저장소에 저장된 버전을 확인할 수 있다.

```bash
git log

# log message
commit fe2dc0fe0d1a3ee6805b86b42f58f169b0a7fea6 (HEAD -> master)
Author: meantint <mistinca@naver.com>
Date:   Sat Oct 9 01:32:00 2021 +0900

    Create test.txt
```

이전에 설정한 `user.name`, `user.email`이 잘 출력되는 것을 확인할 수 있다. 또한 커밋한 날짜 정보를 얻을 수 있고 내가 버전을 만들 때 생성한 메시지도 볼 수 있다.

`(HEAD -> master)`는 이 버전이 가장 최신이라는 것을 알려주는 표시이다.

이번에는 `test.txt` 변경 후 저장해보자.

```bash
git status

# status message
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test.txt
```

`test.txt`가 스테이징 되지 않았고 처음 생성했을 때와는 다르게 `new file`이 아닌 `modified`로 바뀌어있음을 알 수 있다.

## 수정 파일과 최신 버전의 차이 확인하기(git diff)

수정한 파일이 최신 버전과 어떤 차이가 있는지 보기 위해서는 `git diff` 명령어를 쓰면된다.

```bash
# test.txt 최신 버전
hi
```

```bash
# test.txt 수정 파일
hello

bye
```

```bash
git diff

# diff message
diff --git a/test.txt b/test.txt
index 45b983b..57060ad 100644
--- a/test.txt
+++ b/test.txt
@@ -1 +1,3 @@
-hi
+hello
+
+bye
```

`-`는 최신 버전과 비교했을 때 수정 파일에서 빠진 것이고 `+`는 최신 버전과 비교했을 때 추가된 것이다.

## 동시에 여러개 상태 보기, 커밋하기

새로운 파일을 생성하고, 기존에 있던 파일을 수정해보자.

`test1.txt`이라는 새로운 파일을 만들고 `test.txt` 파일을 수정하였다.

```bash
git status

# status message
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test1.txt
```

각각의 상태에 따라 다르게 출력되는 것을 확인할 수 있다.

```bash
git add test.txt test1.txt # Staging test.txt, test1.txt

git status

# status message
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test.txt
        new file:   test1.txt
```

커밋을 해서 새로운 버전을 만들어보자.

```bash
git commit -m "new version" # commit
```

```bash
git log --stat

# log message
commit b0816847d7ce71680037d79beb40b38d6500fa1a (HEAD -> master)
Author: meantint <mistinca@naver.com>
Date:   Sat Oct 9 13:49:01 2021 +0900

    new version

 test.txt  | 6 +++++-
 test1.txt | 1 +
 2 files changed, 6 insertions(+), 1 deletion(-)
```

`git log` 명령어에 `--stat` 옵션을 붙여주면 커밋에 관련된 파일까지 보여준다.

## 상태 정리

- `untracked` : 처음 생성한 파일이 가지는 상태

- `unmodified` : 기존에 있던 파일, 수정할 것이 없는 상태

- `modified` : 기존에 있던 파일, 수정할 것이 있는 상태

- `staged` : `untracked`, `modified` 상태의 파일을 스테이징 했을 때의 상태. 커밋을 하면 `unmodified` 상태가 된다.

### 순서

1. 새로운 파일을 생성한다.

   - [`untracked`]

2. 파일을 스테이징 한다.

   - [`staged`]

3. 파일을 커밋한다.

   - [`unmodified`]

4. 파일을 수정한다.

   - [`modified`]

5. 파일을 스테이징 한다.

   - [`staged`]

6. 파일을 커밋한다.

   - [`unmodified`]

4번 ~ 6번을 계속 반복하면서 버전을 업데이트 시켜 나간다.

## 작업 되돌리기

커밋 취소, 스테이징 한 파일 내리기 등의 작업 되돌리기를 해보자.

### 작업 트리에서 수정한 파일 되돌리기(git restore)

`test.txt` 파일을 변경해보자.

```bash
# test.txt 기존 파일
Hello World!
```

```bash
# test.txt 변경 파일
Hello World!

git restore test
```

변경된 부분이 있기 때문에 `git status`로 상태를 보면 아래와 같다.

```bash
git status

#status message
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test.txt
```

```bash
git restore test.txt
```

`git restore`는 작업트리에 있는 변경 사항을 취소(복구)시켜준다. 다시 한 번 상태를 확인해보자.

```bash
git status

# status message
On branch master
nothing to commit, working tree clean
```

작업 파일의 수정사항이 사라진 것을 확인할 수 있다.

### 스테이징 되돌리기(git restore --staged)

`git restore`은 작업 트리 수정 파일을 되돌려주지만 `git restore --staged`은 스테이징을 취소 해주는 명령어이다.

현재 상태는 다음과 같다.

```bash
git status

# status message
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test.txt
```

명령어를 통해 스테이징된 파일을 취소해보자.

```bash
git restore --staged test.txt
```

다시 상태를 확인하면 다음과 같다.

```bash
git status

# status message
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test.txt
```

다시 작업 트리에서의 수정 상태로 파일이 변경되어 있는 것을 볼 수 있다.

### 최신 커밋 되돌리기(git reset HEAD^)

파일을 스테이징하고 커밋까지 했을 때, 가장 마지막 커밋을 취소하는 명령어를 알아보자.

현재 상태는 다음과 같다.

```bash
# --stat : commit과 관련된 파일들도 추가해서 보여준다.
# --oneline : 한 줄에 각 커밋을 보여준다.
git log --stat --oneline

# log message
0edc4d2 (HEAD -> master) Test (git reset HEAD^)
 test.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
ff7164a Fix test.txt content
 test.txt | 6 +-----
 1 file changed, 1 insertion(+), 5 deletions(-)
```

가장 최신 버전의 커밋 메시지 `git reset HEAD^ TEST`를 볼 수 있고 이전의 커밋 메시지가 `Fix test.txt content`인 것을 알 수 있다.

최신 커밋인 `Test (git reset HEAD^)`를 지워보자.

```bash
git reset HEAD^
```

최신 커밋이 제거되었는지 확인해보자.

```bash
git log --stat --oneline

# log message
ff7164a (HEAD -> master) Fix test.txt content
 test.txt | 6 +-----
 1 file changed, 1 insertion(+), 5 deletions(-)
a2dcf49 Delete test1.txt
 test1.txt | 3 ---
 1 file changed, 3 deletions(-)
```

최신 커밋이 2번째 최신 커밋이었던 `Fix test.txt content`로 바뀐 것을 알 수 있고 이를 통해 기존의 최신 커밋이 제거되었음을 알 수 있다.
