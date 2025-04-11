# Git 설치 

Main Link => https://git-scm.com/

Download Link => https://git-scm.com/downloads/win

1. git 설치 프로그램 다운로드

각자의 운영체제에 맞는 버전을 다운로드 합니다.

![git-001](https://github.com/user-attachments/assets/e03b29bf-b9af-4fe7-9b63-6950911ffda1)

2. 설치 프로그램 실행

3. Only show new options check 해제 후 Next click

![image](https://github.com/user-attachments/assets/18fe0c3a-a79a-4e2f-8bae-3bf5757a3f9c)

4. Select Components & Next click

추가로 설치하고자 하는 항목을 선택합니다.

저는 추가로 선택을 하지 않고 진행했습니다.

5. Git editor 선택 & Next click

Git 을 사용할 기본 에디터를 선택합니다. 

![image](https://github.com/user-attachments/assets/fbb6562b-9537-40ae-b6cc-9a5dcce33fe9)

6. Git 기본 분기 & Next click

git에서 사용 할 기본 분기 이름을 지정할 수 있습니다. 기본은 "master" 입니다.

![image](https://github.com/user-attachments/assets/45035d54-1480-4fc9-b9ed-62f392d730e2)

7. PATH 환경 설정 & Next click

PATH 환경 조정 설정 입니다. 기본 선택으로 진행 했습니다.

![image](https://github.com/user-attachments/assets/867254b8-aab2-4a0b-a1ea-050da8b30405)

8. SSH 실행 도구 선택 & Next click

![image](https://github.com/user-attachments/assets/2817e117-c4ad-4c66-8d99-a85156dc64e6)

9. Open SSL 라이브러리 선택 & Next click

![image](https://github.com/user-attachments/assets/844a1947-f22a-45d2-9f86-f5b20246051b)

10. 줄 바꿈 옵션 선택 & Next click

![image](https://github.com/user-attachments/assets/6bdb2426-b14d-481b-b772-22652ecf958c)

11. Git Bash 실행 터미널 에뮬레이터 선택 & Next click

![image](https://github.com/user-attachments/assets/02ab1d94-d9da-4016-9e7d-23dad2eb8db4)

12. git pull의 기본 동작 선택 & Next click

git pull의 기본 동작을 선택합니다.

git pull 은 원격 저장소에서 변경 사항을 가져와 로컬 브랜치에 병합을 하는 명령어 입니다.

13. Git 자격증명 도우미 선택 & Next click

![image](https://github.com/user-attachments/assets/2538468b-4e42-4fed-b26b-97ee9a4644cc)

14. 추가 옵션 선택 & Install

![image](https://github.com/user-attachments/assets/dee77ead-0656-4950-ac3d-939aea2e78a4)


# Git 설치 확인

cmd 창에서 `git --version` 을 입력합니다.

![image](https://github.com/user-attachments/assets/7dd72e75-2a22-4307-9a1a-0f91764e344e)

# 기본 설정

Git을 사용하기 위해 현재 pc에 사용자 정보를 설정해야 합니다.

```
git config --global user.name "Your Name"

git config --global user.email "you@example.com"
```

[최 상단으로 이동](https://github.com/pmirnc-dev/pds-welcome/wiki/Git-Setting#git-%EC%84%A4%EC%B9%98)

# 참조
## git 설치
* https://sfida.tistory.com/46