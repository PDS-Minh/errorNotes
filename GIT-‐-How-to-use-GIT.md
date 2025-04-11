# Git 사용 방법

git의 동작 구조를 그림으로 표현하면 다음과 같습니다.

![git work](https://i.namu.wiki/i/mGOcwPPFpufxXoG8aekOcDTHkqQuB85P0FbGyo20byibTjAXSomWr5KRYYq4-vLUJa9-Ido0iN0vYppj8TGdk8n5WsTARe2R9mNsAJMwzjA2k1Nq-nueN5djnybzvchX0-vgokH8x5pUYa5rJO4PSg.webp)

**아주 짧게 3줄 요약을 하면 이렇습니다.**

1. 로컬 저장소에서 작업 변경 사항을 저장합니다.(add, commit)
2. 로컬 저장소의 작업 내용을 원격 저장소에 동기화 요청을 합니다.(push)
3. 동기화가 완료되면 최신 변경 사항을 가져옵니다.(pull)

- **저장소 (Repository)**: 프로젝트의 모든 파일과 변경 이력이 저장되는 곳입니다.
- **커밋 (Commit)**: 파일의 스냅샷을 저장하는 단위로, 변경 사항을 기록합니다.
- **브랜치 (Branch)**: 독립적으로 작업을 진행할 수 있는 분기점입니다. 기본 브랜치는 `main` 또는 `master`입니다.
- **스테이징 영역 (Staging Area)**: 커밋 될 파일들을 잠시 보관하는 공간입니다.
- **원격 저장소 (Remote Repository)**: 네트워크를 통해 접근할 수 있는 저장소로, 협업 시에 주로 사용됩니다.

## 로컬 저장소 생성

로컬 저장소를 생성하는 방법은 다음과 같습니다.

1. vscode 에서 터미널을 실행합니다.

2. 다음 git init 을 입력 후 실행하면 끝 입니다.

```
D:\my-test\nodejs-guide> git init
Initialized empty Git repository in D:/my-test/nodejs-guide/.git/
```

git repository가 생성됐다는 메세지가 나옵니다.

실제로 프로젝트 폴더로 가면 .git 폴더가 생성된 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/d48ad321-8105-4a87-bd37-a34f1cb8733f)

로컬 git 저장소는 3가지 영역으로 나뉘어 있습니다.

1. 작업 디렉토리(Working Directory)
2. 인덱스(Index)
3. 헤드(HEAD)

**작업 디렉토리**는 실제 파일들로 이루어져 있습니다.

**인덱스**는 준비 영역(staging area)

**헤드**는 최종 확정본(commit) 영역입니다

먼저 변경사항이 있는 파일에 대해 인덱스(index)에 추가(add) 합니다.

commit은 로컬 저장소에 현재 작업 중인 폴더에 있는 모든 파일에 대한 변경사항을 기록합니다.

### gitignore 생성

여기서 한가지 문제점이 있습니다. node_modules에는 방대한 양의 패키지들이 설치되는데 이를 git에 같이 저장하기엔 용량이 너무 큽니다.

또한 비밀을 유지해야 하는 숨김 파일 같은 항목을 git에 저장하지 않게 하려면 gitignore 파일이 필요합니다.

탐색기에서 .gitignore 파일을 생성합니다.

직접 입력할 수도 있지만 쉽게 생성해주는 사이트도 있습니다. 

Link => https://www.toptal.com/developers/gitignore

운영체제, 개발환경, 언어 혹은 도구를 입력하고 생성 버튼을 누르면 .gitignore에 입력 할 내용이 생성됩니다.

![image](https://github.com/user-attachments/assets/5f50a94d-0b4c-4656-8d91-9d584c39efa5)

그대로 복사 & 붙여넣기 해줍니다.


```
# Created by https://www.toptal.com/developers/gitignore/api/windows,visualstudiocode,node
# Edit at https://www.toptal.com/developers/gitignore?templates=windows,visualstudiocode,node

### Node ###
# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
lerna-debug.log*
.pnpm-debug.log*

... 너무 길어서 중략

```

## git 상태 확인하기

최초 혹은 파일의 내용이 변경되면 git이 자동으로 감지합니다. 

터미널 명령어로도 확인을 할 수 있지만 vs code 화면 위주로 설명을하겠습니다.

### add

vs code 의 좌측에 보면 소스 제어 탭이 있습니다. 이 항목을 클릭하면 소스 제어 화면이 나옵니다.

변경 사항에 내용이 변경 된 파일들의 목록이 보입니다. 

처음 git을 세팅하면 등록 된 파일이 없기 때문에 모두 추가해야 합니다.

변경 사항에 마우스를 올리면 + 가 나오는데 일괄 추가 할 수 있고, 개별 파일별로 추가할 수 있습니다.

![image](https://github.com/user-attachments/assets/ebf1eaac-b29f-4eba-a049-26806539cd50)

변경 사항에 있는 항목들이 스테이징된 변경 사항으로 이동 된 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/f5cd7bba-a64c-4690-851d-3348cea65651)

### commit

스테이징에 있는 파일들을 commit 해야 합니다. 

commit은 스테이징된 파일들의 스냅샷을 로컬 저장소에 저장하게 해줍니다. 

commit을 통해 변경 이력을 남기고, 이후에 특정 시점으로 되돌아가거나 다른 사람들과 협업할 때 중요한 역할을 합니다.

commit을 할 때는 메세지를 통해 내가 어떤 작업을 했는지 기록하면 확인을 하기 쉬우므로 메세지를 남기는 것을 권장합니다.

메세지를 남길 때 규칙은 다음과 같습니다.

```
타입(스코프): 주제(제목) // Header

본문 // Body

바닥글 // Footer
```

**Header** 는 필수이며 scope는 생략 가능합니다.

타입은 커밋이 어떤 내용인지 나타내는 라벨 입니다.

아래의 항목들 중 자주 쓰이는 항목은 feat, fix, docs 정도 입니다.


| 타입 이름    | 내용                               |
|----------|----------------------------------|
| feat     | 새로운 기능에 대한 커밋                    |
| fix      | 버그 수정에 대한 커밋                     |
| build    | 빌드 관련 파일 수정 / 모듈 설치 또는 삭제에 대한 커밋 |
| chore    | 그 외 자잘한 수정에 대한 커밋                |
| ci       | ci 관련 설정 수정에 대한 커밋               |
| docs     | 문서 수정에 대한 커밋                     |
| style    | 코드 스타일 혹은 포맷 등에 관한 커밋            |
| refactor | 코드 리팩터링에 대한 커밋                   |
| test     | 테스트 코드 수정에 대한 커밋                 |
| perf     | 성능 개선에 대한 커밋                     |

**Body** 는 Header의 내용을 뒷받침 한 상세한 내용을 적습니다.

Header에서 충분히 설명 가능하다면 생략해도 됩니다.


**Footer** 는 바닥글로 어떤 이슈에서 왔는지 참조정보들을 추가하는 용도로 사용합니다.

Footer 또한 생략 가능합니다.

vscode 에서 해보겠습니다.

저는 메세지 입력 칸에 `feat: first commit` 으로 입력했습니다.

![image](https://github.com/user-attachments/assets/ed1bb02c-b122-4e62-a1aa-869c5c74de51)

여기서 commit button 오른쪽 화살표를 클릭하면 옵션이 나옵니다. 

![image](https://github.com/user-attachments/assets/e09b0b45-98c8-4be2-82a5-de15d84298fa)

커밋(commit) 은 로컬 저장소에 저장하는 것 이고 커밋 및 푸시(commit and push)는 로컬 저장소에 저장 후 원격 저장소로 동기화 요청을 하는 것 입니다.

먼저 commit 부터 하고 원격 저장소는 뒤에 이어서 설명하겠습니다.

commit을 하면 소스 제어 그래프, repository 탭에 commit을 한 내용이 기록됩니다.

![image](https://github.com/user-attachments/assets/53c80621-68a7-405e-820e-9bbc5bb49ae7)

## 원격 저장소

### GitHub

GitHub란 git을 기반으로 한 웹 서비스로, 프로젝트를 관리하고 협업할 수 있는 플랫폼 입니다. 

github 외에 GitLab, Bitbucket, SoruceForge, Azure DevOps Repos 등등이 있습니다.

repository 는 프로젝트 저장소 이며, git push 를 하게되면 repository에 저장이 됩니다.

### remote 설정

vs code 에서 원격 repository를 추가를 하는 방법은 간단합니다.

소스 제어에서 ... 클릭 > 원격 > 원격 추가 입니다.

화면 상단에 원격 주소를 입력하는 창이 나오면 연결하고자 하는 github 주소를 입력합니다.

https://github.com/pmirnc-dev/pds-welcome.git

![image](https://github.com/user-attachments/assets/0625661e-5019-4b46-bde7-23607192ccc7)

원격 이름을 입력하라고 나오는데 기본은 origin 을 입력하면 됩니다.

![image](https://github.com/user-attachments/assets/c8c443a9-d853-47fa-9aed-4b5c97d9ec88)

### push

연결이 성공하면 Remotes 에 origin으로 원격 저장소가 연결 된 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/6cea1a21-e4cf-4f49-8045-d2ca059521b4)

게시 Branch 버튼을 클릭하면 원격 저장소로 작업물이 저장 됩니다.

![image](https://github.com/user-attachments/assets/4af36ff2-340b-4512-a309-b0c9417fdef0)

## 협업하기

프로젝트를 혼자 진행하면 branch를 어떻게 사용하던 상관 없습니다.

그러나 팀으로 작업을 할 경우엔 다른 사림이 작업한 코드를 실수로 수정하거나 삭제하는 등 문제가 발생할 수 있습니다.

이를 방지하기 위해 협업하는 방법을 알아보겠습니다.

### clone

프로젝트 매니저가 원격 repository를 생성 할 것 입니다.

여러분은 원격 git url을 로컬 프로젝트로 복사해야 합니다.

프로젝트를 생성하고자 하는 폴더로 이동 합니다.

![image](https://github.com/user-attachments/assets/b65f57eb-237c-4657-a757-8824127389f1)

폴더에서 아무 곳이나 마우스 우클릭 > Open Git Bash here 를 선택합니다.

터미널 창이 나오고 프로젝트를 복사하기 위해 다음 명령어를 입렵합니다.
```
git clone https://github.com/pmirnc-dev/pds-welcome.git
```

![image](https://github.com/user-attachments/assets/654c88c0-0a3d-4ffe-acbe-2e3340d34186)

프로젝트 복사가 성공하면 탐색기에 원격 repository 이름으로 폴더가 생성 된 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/4f45d7d3-bf99-4a01-a0d2-5a66099902a6)

vscode를 사용하여 새로운 프로젝트를 열어봅시다.

파일 > 폴더열기를 선택 후 새로운 프로젝트 폴더를 열어줍니다.

### branch

예를 들어봅시다. 

게시판을 조회하는 코드에 오류가 발생하여 수정해야 합니다.

main branch에 직접 수정을 해도 되지만, 다른 팀원과 작업 영역이 겹칠 수 있기 때문에 작업 영역을 분리해야 합니다.

이 때 필요한 것이 branch 분기 입니다.

1. 분기하려는 branch 우클릭 -> Create branch

![image](https://github.com/user-attachments/assets/4a4199dd-01d0-4338-b9fc-6224cadf5a50)

2. brach 이름 입력

PMI에서 사용하는 branch 명명 규칙은 두가지 입니다.

    1. 사용자 이니셜/작업명
    2. #이슈번호-작업명

![image](https://github.com/user-attachments/assets/dcdde509-a108-43ba-b8fa-0b72a8ec84bb)

3.  3가지 선택지가 나옵니다. Create & Switch to Branch 를 하면 브랜치 성성 및 새로 생성한 브랜치로 이동이 됩니다.

![image](https://github.com/user-attachments/assets/cbb67fef-91bb-457e-a87c-b87aa7479279)

4. 새로 생성된 branch

![image](https://github.com/user-attachments/assets/40b21ba2-fa87-43bb-99f7-64e70e6a3de9)

## Pull Request(PR)

이제 작업 branch 에서 수정 한 내용들을 master(main) branch 에 병합을 해야 합니다.

Pull Request는 개발자들이 자신이 작업한 작업물을 다른 팀원들에게 검토하고 병합을 요청하는 기능 입니다.

ihhwang/branch_test 에서의 작업물을 원격 저장소로 push 하겠습니다.

push를 하면 github에 노란색 공간이 하나 생기고 Compare & pull request 버튼을 클릭합니다.

![image](https://github.com/user-attachments/assets/0eff2c5d-d1cd-44fc-9543-7f3a363ef553)

Open pull request 화면으로 넘어가면서 내 작업물에 대한 설명을 추가 할 수 있고, 하단에는 변경사항이 나와있습니다.

![image](https://github.com/user-attachments/assets/993cda2c-ecb9-46da-94a5-613c383cbea9)

Create pull request 버튼을 클릭하면 github 에서 자동으로 conflict 체크를 합니다.

![image](https://github.com/user-attachments/assets/f3b2ed13-0c77-487f-9445-25dd1ab258eb)

작업물에 이상이 없다면 Merge pull request 버튼을 클릭하여 master branch에 ihhwang/branch_test 를 병합합니다.

![image](https://github.com/user-attachments/assets/8377e8aa-011e-432d-9492-9f5fb28004af)

mrege가 완료되면 보라색으로 Merged 상태로 바뀌며 branch 삭제여부도 나옵니다.

더이상 사용하지 않을거라면 깔끔하게 삭제를 하고 계속 이어서 작업을 하려면 그냥 두시면 됩니다.

![image](https://github.com/user-attachments/assets/9189014d-9611-479f-8a24-a3e7269f2d6a)

## Pull

master branch에 새로운 변경사항이 병합됐으므로 master branch의 상태가 변합니다

master 또한 동기화를 해줘야 하므로 master branch로 checkout 합니다. 

![image](https://github.com/user-attachments/assets/8a620a8f-bfbf-49b0-8025-d8fcbccbf3bd)

변경내용 동기화를 하면 master 에도 index.html, main.js가 생성됩니다.

![image](https://github.com/user-attachments/assets/0f284ee9-01e7-49ed-840f-c0ab32abb17c)

## Conflict
가끔 작업을 하다보면 같은 코드를 수정하고 branch를 병합하면 충돌이 발생하는 경우가 있습니다.

처음 겪게되면 무척 당황스러운데 걱정 할 필요 없습니다. (업무 분담 및 소통의 중요성)


충돌 상황을 재연하기 위해 먼저 master 에서 main.js에 코드를 한 줄 수정 후 push까지 진행하겠습니다.

그 다음 다른 branch로 이동하여 똑같은 부분을 다른 코드로 수정해봅니다.

![image](https://github.com/user-attachments/assets/4561bd78-7b7d-461b-80b8-cd5cbd0eacda)

아까와는 다르게 Conflict 라고 메세지가 나오는 것을 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/ddc2225b-2921-4311-95aa-15a2442d663b)

Resolve conflicts 를 클릭하여 확인해봅니다.

![image](https://github.com/user-attachments/assets/7a638456-2cad-41a3-aaf8-ace50f92384c)

======= 을 기준으로 위는 ihhwang/branch_test 이고 아래는 master 입니다.

최종적으로 남길 코드를 자유롭게 편집합니다.

수정을 하고 우측에 Mark as resolved 를 클릭하면 commit mrege 로 변합니다.

![image](https://github.com/user-attachments/assets/bd494dfa-4d5d-4b20-b295-e666bfbefcc2)

conflict test를 통과했고 Merge를 할 수 있습니다.

![image](https://github.com/user-attachments/assets/894daca9-c5c8-4585-93d2-d2f5131972e8)

