**목차**

:rocket:[이전 내용 간단 복습](#pushpin-이전-내용-간단-복습)

:rocket:[Branch](#pushpin-branch)

:rocket:[Fork](#pushpin-fork)

:rocket:[기타 명령어](#pushpin-기타-명령어)


# :pushpin: 이전 내용 간단 복습
##  프로젝트 시작할 때 
```bash
git init
```

* git init하면 (main)으로 확인할 수 있음

<br>

## 버전 기록할 때
```bash
git add .
git commit -m '커밋메시지'
```

* git status로 파일 상태 확인 해보기 
* git log로 커밋 확인하기

<br>

## 원격저장소 최초 설정할 때
```bash
git remote add origin url
```

<br>

## 원격저장소 활용
### push
git push origin main

- `origin` : 원격저장소의 이름
- `main` : 브랜치의 이름

* 참고 : github.io repository 만들고 그 안에 html이나 css를 넣어서 github에서 제공해주는 서버를 이용할 수 있다.*

### pull
```bash
git pull origin main
```

<br>

---

<br>

# :pushpin: Branch
    독립적인 작업흐름을 만들고 관리

## 1. 명령어
1. `git branch`
    - 현재 브랜치 목록을 보여줍니다.
    - 현재 어떤 브랜치에 있는지도 확인할 수 있습니다.
2. `git branch <branch-name>`
    - 새로운 브랜치를 생성합니다.
    - `<branch-name>`에 새로운 브랜치의 이름을 입력합니다.
3. `git branch -d <branch-name>`
    - 브랜치를 삭제합니다.
    - -d 옵션은 브랜치를 삭제할 때 사용합니다.
4. `git branch -D <branch-name>`
    - 강제로 브랜치를 삭제합니다.
    - -D 옵션은 변경사항이 있더라도 브랜치를 삭제합니다.
5. `git branch -m <new-branch-name>`
    - 현재 브랜치의 이름을 변경합니다.
    - -m 옵션 다음에 새로운 브랜치 이름을 입력합니다.
6. `git checkout <branch-name>`
    - 다른 브랜치로 전환합니다.
    - `<branch-name>`에 전환하고자 하는 브랜치의 이름을 입력합니다.
7. `git checkout -b <new-branch-name>`
    - 새로운 브랜치를 생성하고 해당 브랜치로 전환합니다.
    - -b 옵션 다음에 새로운 브랜치 이름을 입력합니다.
8. `git merge <branch-name>`
    - 다른 브랜치를 현재 브랜치로 병합합니다.
    - `<branch-name>`은 병합하고자 하는 브랜치의 이름입니다.
9. `git rebase <branch-name>`
    - 현재 브랜치를 `<branch-name>` 브랜치의 최신 커밋 위로 재배치합니다.
10. `git cherry-pick <commit>`
    - 다른 브랜치의 특정 커밋을 현재 브랜치로 가져옵니다.
    - `<commit>`에 가져올 커밋의 해시값을 입력합니다.

<br>


## 2. git을 사용할 때 유의할 점
1. master branch는 반드시 배포 가능한 상태
2. feature branch는 각 기능의 의도를 알 수 있도록
3. pull request 통해 협업
4. commit message는 명확하게 쓰자
5. 변경사항을 반영하고 싶다면 master branch에 merge하자

<br>

## 3. PR
주로 오픈 소스 프로젝트 또는 팀 협업에서 사용되며, 코드 변경 사항을 검토하고 병합하기 전에 다른 개발자들의 의견을 얻을 수 있는 방법 중 하나입니다.
<br>

1. main 브랜치는 직접 push 할 수 없도록 막아뒀다. -> PR로만 가능
2. 리뷰가 필수인 경우 -> 꼭 리뷰어를 3명을 반드시 통과해야만 PR를 Merge 버튼 활성화
3. 관리자(시니어 급만) Merge를 하도록 하기도 한다.

<br>

### PR(Pull Request) 생성 과정
1. 새로운 브랜치 생성: 먼저 작업할 내용을 위한 새로운 브랜치를 생성합니다. 이 브랜치를 "소스 브랜치"라고 부릅니다.

2. 코드 변경: 소스 브랜치에서 코드 변경 작업을 진행합니다. 버그 수정, 새로운 기능 추가 등을 포함할 수 있습니다.

3. 커밋: 변경 사항을 커밋하여 로컬 저장소에 저장합니다. 변경 내용이 완료되면 해당 브랜치에 커밋합니다.

4. 원격 저장소에 푸시: 커밋한 변경 사항을 원격 저장소로 푸시합니다. 원격 저장소의 동일한 이름의 브랜치에 변경 사항이 반영됩니다.

5. PR 생성: 원격 저장소에서 Pull Request(이하 PR)을 생성합니다.
    - PR을 생성할 때 어떤 브랜치에서 어떤 브랜치로 병합할 것인지를 설정합니다.
    - PR에는 변경 사항에 대한 간단한 요약 및 설명을 추가할 수 있습니다.

<br>

### PR(Pull Request) 병합(Merge) 과정

1. PR 리뷰: PR을 생성하면 다른 개발자들이 변경 사항을 검토하고 의견을 제시합니다. 리뷰어들은 변경 내용을 확인하고 수정 사항을 요청할 수 있습니다.

2. 코드 수정: 리뷰어들의 의견에 따라 코드를 수정하거나 변경합니다. 이때 추가 커밋을 생성하여 수정 내용을 커밋합니다.

3. 테스트 및 빌드: PR이 생성될 때마다 자동으로 테스트와 빌드가 수행됩니다. 이를 통해 코드의 안정성과 품질을 검증합니다.

4. PR 승인: 리뷰어들이 만족할만한 결과물이라면, PR을 승인합니다. 승인이 된 경우에만 PR을 병합할 수 있습니다.

5. PR 병합(Merge): 승인된 PR을 병합합니다.
    - 이로써 소스 브랜치의 변경 사항이 타겟 브랜치에 통합됩니다.
    - 병합시 충돌이 발생할 수 있으며, 이 경우 충돌을 해결해야 합니다.

6. PR 닫기: PR이 성공적으로 병합되면 해당 PR을 닫습니다. 이후 PR에서의 변경 사항은 해당 타겟 브랜치에 반영됩니다.

<br>

## 4. Branch 정리
1. 작업하기 전에 브랜치를 만든다.
    - `git branch 브랜치이름`
    - `git checkout 브랜치이름`
2. 브랜치에서 코딩
3. 버전을 기록한다 (커밋)
    - `git add .`
    - `git commit -m ""`
4. 작업이 끝나면, 작업한 브랜치를 push
    - `git push origin <브랜치이름>`
5. GitHub에서 Pull Request를 생성한다.
6. 코드리뷰 등 협업 룰에 따라서 진행하고 다 완료되면 merge가 GitHub에서 된다.

<br>

---

<br>

# :pushpin: Fork 
1. Fork 대상 저장소 찾기
    - 복제하고자 하는 원격 저장소(프로젝트)를 찾습니다. 이는 다른 사람이 생성한 프로젝트일 수 있습니다.

2. Fork 버튼 클릭
    - 대상 저장소의 페이지로 이동하여, 화면 상단 우측에 있는 "Fork" 버튼을 클릭합니다.

3. Fork 선택 및 복제
    - "Fork" 버튼을 클릭하면, 해당 프로젝트가 자신의 계정으로 복제됩니다. 이 때, "Fork" 버튼의 아이콘이나 문구는 플랫폼마다 조금 다를 수 있습니다.

4. Fork된 저장소 확인
    - 자신의 계정으로 복제된 저장소를 확인할 수 있습니다. 이 저장소는 원본 프로젝트와 독립적으로 관리됩니다.

5. 로컬에서 작업
    - Fork된 저장소를 로컬 환경으로 클론(Clone)하고, 이를 통해 코드 변경 작업을 진행합니다. 이때 소스 브랜치에서 작업을 수행하며, 변경 사항을 커밋하고 푸시(Push)합니다.

6. 변경 사항 Push
    - 변경한 내용을 로컬에서 원격 저장소로 푸시합니다. 이로써 **자신의 계정의 원격 저장소에 변경 내용이 업로드됩니다.**

7. Pull Request 생성
    - GitHub에서 Pull requests 누르고 create하면 된다.
    - 변경한 내용을 원본 프로젝트에 반영하고자 할 때, 원본 프로젝트로 Pull Request(이하 PR)을 생성합니다. 이 PR에 변경 내용을 요약하고 설명을 추가합니다.

8. PR 리뷰 및 수정
    - 원본 프로젝트의 관리자나 다른 개발자들이 PR을 리뷰하고 의견을 제시합니다. 이 의견을 반영하여 코드를 수정하고 추가 커밋을 생성합니다.

9. PR 병합(Merge)
    - 원본 프로젝트 관리자가 PR을 검토하고 승인하면, PR을 병합(Merge)하여 변경 사항을 원본 프로젝트에 반영합니다.

---

# :pushpin: 기타 명령어
## git add를 취소할 경우
```bash
git restore --staged <file>

#ex
git restore .
```
    
<br>

## 커밋 메시지를 변경하는 경우
```bash
git commit --amend
```
- 위의 명령어를 실행하면, 이전 커밋 메시지로 수정할 수 있는 텍스트 에디터가 열린다. 수정, 변경 후 편집기를 종료하면 해당 커밋의 메시지가 종료된다. *hash 값도 바뀜 -> 버전이 바뀐다*
    - vi인 경우,
        - 수정 시작 : 아무 키나 누르면 수정 시작
        - 종료 방법 : `ESC버튼 -> :wq`
    - 터미널에서 `git config --global core.editor "code --wait"`으로 설정하면 더 쉽게 수정가능
- 이미 공유된 커밋 메시지를 변경하는 것은 신중할 필요가 있다.. 잘못하면 merge conflict가 발생! 그러니 되도록이면 바꾸지 말자..


<br>

## 커밋을 취소하는 경우
```bash
git reset HEAD~ #최근 커밋 취소하기
git reset <commit> #특정 커밋 취소하기
git resuet <commit> --hard # --hard 모드 사용하면 해당 커밋 이후의 변경내용까지 삭제된다. 워킹디렉토리까지 해당 커밋 상태로 되돌아가니 주의하자.
```

## 추가로 더 찾아볼 것
1. `git revert`