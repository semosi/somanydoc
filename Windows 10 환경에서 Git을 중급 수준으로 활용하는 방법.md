---
tags:
  - github
---
 Windows 10 환경에서 Git을 중급 수준으로 활용하는 방법을 매뉴얼 형태로 자세히 설명해 드리겠습니다. 이 매뉴얼은 Git의 기본적인 개념을 알고 있다고 가정하며, 브랜칭, 병합, 충돌 해결, 원격 저장소 관리, 그리고 작업 되돌리기 등 실질적인 협업과 프로젝트 관리에 필요한 기능들을 다룹니다.

---

## Git 활용 매뉴얼 (Windows 10, 중급편)

### 목차

1.  **시작하기 전에: Git 설치 및 초기 설정**
    *   1.1 Git 설치
    *   1.2 Git 초기 사용자 설정
    *   1.3 기본 텍스트 에디터 설정
    *   1.4 기본 브랜치 이름 설정

2.  **Git 기본 개념 복습 (빠른 요약)**
    *   2.1 작업 디렉토리 (Working Directory)
    *   2.2 스테이징 영역 (Staging Area / Index)
    *   2.3 로컬 저장소 (Local Repository)
    *   2.4 원격 저장소 (Remote Repository)

3.  **로컬 저장소 관리 (기본 & 심화)**
    *   3.1 새 저장소 생성 (`git init`)
    *   3.2 기존 저장소 클론 (`git clone`)
    *   3.3 파일 상태 확인 (`git status`)
    *   3.4 변경 사항 스테이징 (`git add`)
    *   3.5 변경 사항 커밋 (`git commit`)
    *   3.6 커밋 히스토리 확인 (`git log`)
    *   3.7 `.gitignore` 파일 활용

4.  **브랜치(Branch) 관리: 협업의 핵심**
    *   4.1 브랜치란?
    *   4.2 브랜치 생성 및 전환 (`git branch`, `git checkout`, `git switch`)
    *   4.3 브랜치 목록 확인
    *   4.4 브랜치 병합 (`git merge`)
    *   4.5 병합 충돌 (Merge Conflict) 해결
    *   4.6 브랜치 삭제 (`git branch -d`)

5.  **원격 저장소(Remote Repository) 연동**
    *   5.1 원격 저장소 확인 (`git remote`)
    *   5.2 원격 저장소 추가/제거 (`git remote add/remove`)
    *   5.3 원격 저장소의 변경 사항 가져오기 (`git fetch`)
    *   5.4 로컬 저장소 업데이트 (`git pull`)
    *   5.5 로컬 변경 사항 원격 저장소에 반영 (`git push`)
    *   5.6 SSH 키 설정 (선택 사항, 권장)

6.  **작업 되돌리기 (Undo Changes)**
    *   6.1 작업 디렉토리 변경 취소 (`git restore`)
    *   6.2 스테이징 영역 변경 취소 (`git restore --staged`)
    *   6.3 커밋 되돌리기 (`git reset`)
        *   `--soft`
        *   `--mixed` (기본값)
        *   `--hard` (주의!)
    *   6.4 커밋 내용 수정 (`git commit --amend`)
    *   6.5 특정 커밋 취소 (`git revert`)
    *   6.6 작업 임시 저장 (`git stash`)

7.  **고급 Git 활용 (Rebase, Tag)**
    *   7.1 리베이스(Rebase): 히스토리 정렬 (`git rebase`)
        *   주의사항
    *   7.2 태그(Tag): 중요 시점 표시 (`git tag`)

8.  **Git GUI 도구 (선택 사항)**
    *   8.1 Git GUI
    *   8.2 Sourcetree, GitKraken, VS Code 등

9.  **문제 해결 및 팁**
    *   9.1 자주 발생하는 문제
    *   9.2 유용한 Git 명령어 별칭(Alias) 설정
    *   9.3 좋은 커밋 메시지 작성법

---

### 1. 시작하기 전에: Git 설치 및 초기 설정

Git을 사용하기 전에 Windows 10 시스템에 Git을 설치하고 초기 설정을 완료해야 합니다.

#### 1.1 Git 설치

1.  **Git 공식 웹사이트 방문:** [https://git-scm.com/download/win](https://git-scm.com/download/win) 에 접속합니다.
2.  **설치 파일 다운로드:** 최신 버전의 "64-bit Git for Windows Setup"을 다운로드합니다.
3.  **설치 실행:** 다운로드한 `.exe` 파일을 실행합니다.
4.  **설치 옵션:**
    *   기본 설정을 대부분 유지해도 무방합니다.
    *   **"Select Components"**: `Git Bash Here` 와 `Git GUI Here` 가 기본으로 선택되어 있는지 확인합니다.
    *   **"Adjusting your PATH environment"**: `Git from the command line and also from 3rd-party software` (두 번째 옵션)를 선택하는 것이 좋습니다. 이렇게 하면 Git 명령어를 Windows 명령 프롬프트(CMD)나 PowerShell에서도 사용할 수 있습니다.
    *   **"Choosing the default editor used by Git"**: Visual Studio Code, Notepad++, Sublime Text 등 선호하는 에디터를 선택할 수 있습니다. 기본값은 Vim이지만, 익숙하지 않다면 다른 에디터를 선택하는 것이 좋습니다. (이 설정은 나중에 변경 가능합니다.)
    *   나머지 옵션은 기본값을 유지하고 "Next"를 클릭하여 설치를 완료합니다.

5.  **설치 확인:**
    *   명령 프롬프트(CMD) 또는 PowerShell을 열고 다음 명령어를 입력합니다.
        ```bash
        git --version
        ```
    *   Git 버전 정보가 출력되면 성공적으로 설치된 것입니다.

#### 1.2 Git 초기 사용자 설정

Git은 커밋할 때 사용자 정보(이름, 이메일)를 기록합니다. 이 정보는 모든 커밋에 포함되므로, 최초 1회만 설정하면 됩니다.

```bash
git config --global user.name "당신의 이름"
git config --global user.email "당신의 이메일@example.com"
```
*   `--global` 옵션은 해당 시스템의 모든 Git 저장소에 적용됩니다. 특정 저장소에만 다른 정보를 사용하고 싶다면 `--global` 옵션을 제외하고 해당 저장소 디렉토리에서 설정하면 됩니다.

#### 1.3 기본 텍스트 에디터 설정

Git이 커밋 메시지나 병합 충돌 등을 처리할 때 사용할 기본 텍스트 에디터를 설정합니다. (설치 시 선택한 에디터가 마음에 들지 않을 경우 변경)

*   **VS Code로 설정:**
    ```bash
    git config --global core.editor "code --wait"
    ```
*   **Notepad++로 설정 (경로 확인 필요):**
    ```bash
    git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
    ```
    *   `'...'`와 같이 경로에 공백이 있는 경우 따옴표로 감싸야 합니다.

#### 1.4 기본 브랜치 이름 설정A

Git 2.28 버전부터는 초기 브랜치 이름을 `master`에서 `main`으로 변경하는 것이 권장됩니다.

```bash
git config --global init.defaultBranch main
```
*   이 설정은 `git init`으로 새 저장소를 만들 때 적용됩니다. 기존 저장소에는 영향이 없습니다.

---

### 2. Git 기본 개념 복습 (빠른 요약)

Git의 워크플로우를 이해하기 위한 핵심 개념입니다.

*   **2.1 작업 디렉토리 (Working Directory):** 실제 프로젝트 파일들이 있는 곳입니다. Git이 추적하는 파일과 추적하지 않는 파일(`.gitignore`에 명시된 파일 등)이 모두 존재합니다.
*   **2.2 스테이징 영역 (Staging Area / Index):** 커밋할 준비가 된 파일들이 임시로 대기하는 곳입니다. `git add` 명령으로 파일이 이 영역으로 이동합니다.
*   **2.3 로컬 저장소 (Local Repository):** `git commit` 명령으로 스테이징 영역의 변경 사항들이 영구적으로 저장되는 곳입니다. 모든 커밋 히스토리가 기록됩니다. `.git`이라는 숨김 폴더 내에 저장됩니다.
*   **2.4 원격 저장소 (Remote Repository):** GitHub, GitLab, Bitbucket 등 외부에 있는 서버에 위치한 저장소입니다. 여러 개발자가 협업하고 코드를 공유하는 중앙 저장소 역할을 합니다.

```
Working Directory --- (git add) ---> Staging Area --- (git commit) ---> Local Repository --- (git push) ---> Remote Repository
                                                                   <--- (git pull) ---
```

---

### 3. 로컬 저장소 관리 (기본 & 심화)

#### 3.1 새 저장소 생성 (`git init`)

새 프로젝트를 Git으로 관리하고 싶을 때 사용합니다.

```bash
# 프로젝트 폴더로 이동
cd C:\Users\YourUser\Documents\MyNewProject

# 현재 폴더를 Git 저장소로 초기화
git init
```
*   폴더 안에 `.git` 이라는 숨김 폴더가 생성되며, Git 관리가 시작됩니다.

#### 3.2 기존 저장소 클론 (`git clone`)

원격 저장소에 있는 프로젝트를 로컬로 복사해올 때 사용합니다.

```bash
# GitHub 등에서 제공하는 저장소 URL (HTTPS 또는 SSH)
git clone https://github.com/username/repository-name.git
# 또는
git clone git@github.com:username/repository-name.git

# 특정 폴더에 클론하고 싶다면 폴더명 지정
git clone https://github.com/username/repository-name.git MyLocalFolder
```
*   클론된 폴더는 자동으로 `.git` 폴더를 포함하며, 원격 저장소와 연결됩니다.

#### 3.3 파일 상태 확인 (`git status`)

현재 작업 디렉토리와 스테이징 영역의 상태를 보여줍니다. 어떤 파일이 수정되었고, 스테이징되었는지, 커밋되지 않았는지 등을 알 수 있습니다.

```bash
git status
```
*   **출력 예시:**
    *   `Untracked files:`: Git이 아직 추적하지 않는 새 파일
    *   `Changes not staged for commit:`: 수정되었으나 아직 `git add` 하지 않은 파일
    *   `Changes to be committed:`: `git add` 되어 커밋 대기 중인 파일

#### 3.4 변경 사항 스테이징 (`git add`)

수정되거나 새로 추가된 파일을 커밋에 포함시키기 위해 스테이징 영역에 추가합니다.

```bash
# 특정 파일 스테이징
git add index.html

# 특정 폴더 내 모든 파일 스테이징
git add css/

# 현재 디렉토리의 모든 변경 사항 스테이징 (새 파일, 수정된 파일 모두 포함)
git add .

# 특정 파일의 특정 변경 부분만 스테이징 (대화형 모드)
git add -p [파일명]
```

#### 3.5 변경 사항 커밋 (`git commit`)

스테이징 영역에 있는 파일들을 로컬 저장소에 영구적으로 기록합니다.

```bash
# 커밋 메시지와 함께 커밋
git commit -m "feat: 로그인 기능 구현"

# 커밋 메시지 작성을 위해 에디터 열기
git commit

# 이전 커밋 메시지 수정 및 현재 스테이징된 변경 사항 추가 (커밋 히스토리 수정)
git commit --amend
```
*   **좋은 커밋 메시지:** 간결하고 명확하게 어떤 변경 사항이 있었는지 설명해야 합니다. (예: `type: subject` 형식)

#### 3.6 커밋 히스토리 확인 (`git log`)

저장소의 커밋 기록을 확인합니다.

```bash
# 전체 커밋 히스토리 확인
git log

# 간략하게 한 줄로 요약
git log --oneline

# 그래프 형태로 브랜치 및 병합 히스토리 확인
git log --oneline --graph --all

# 특정 사용자 커밋만 확인
git log --author="당신의 이름"

# 특정 기간 커밋만 확인
git log --since="2 weeks ago"
```

#### 3.7 `.gitignore` 파일 활용

Git이 특정 파일이나 폴더를 추적하지 않도록 설정하는 파일입니다. 빌드 파일, 로그 파일, 임시 파일, 설정 파일 등 저장소에 포함시키고 싶지 않은 파일들을 명시합니다.

1.  **파일 생성:** 프로젝트 루트 디렉토리에 `.gitignore` 파일을 생성합니다.
2.  **내용 작성:** 무시할 파일 또는 폴더 패턴을 각 줄에 작성합니다.

    ```
    # 주석은 #으로 시작합니다.

    # 특정 파일 무시
    .DS_Store
    .env

    # 특정 확장자 파일 무시
    *.log
    *.temp

    # 특정 폴더와 그 내용 무시
    node_modules/
    dist/

    # 특정 폴더 내의 모든 파일 무시 (폴더 자체는 남아있음)
    build/*

    # 특정 폴더는 무시하지만, 그 안의 특정 파일은 추적
    !build/index.html
    ```
*   `git init` 후 또는 `git clone` 후 `.gitignore` 파일을 만들거나 수정하면, Git은 해당 파일들을 더 이상 추적하지 않습니다. 이미 추적 중인 파일을 `.gitignore`에 추가하려면, 먼저 Git의 추적을 해제해야 합니다: `git rm --cached <파일/폴더명>` 후 다시 `git add .` 및 `git commit` 합니다.

---

### 4. 브랜치(Branch) 관리: 협업의 핵심

브랜치는 독립적인 작업 공간을 제공하여 여러 개발자가 동시에 다른 기능을 개발하거나 버그를 수정할 수 있게 합니다.

#### 4.1 브랜치란?

포인터와 같습니다. Git은 커밋들을 연결된 스냅샷 체인으로 저장하며, 브랜치는 단순히 이 체인의 특정 커밋을 가리키는 레이블입니다.

#### 4.2 브랜치 생성 및 전환

*   **새 브랜치 생성:**
    ```bash
    git branch feature/login
    ```
    *   이 명령어는 현재 브랜치의 최신 커밋을 가리키는 `feature/login`이라는 새 포인터를 만듭니다.

*   **브랜치 전환 (이동):**
    ```bash
    git checkout feature/login
    # 또는 Git 2.23+ 버전부터 권장되는 명령어
    git switch feature/login
    ```
    *   이 명령어를 사용하면 작업 디렉토리의 파일들이 해당 브랜치의 최신 커밋 상태로 변경됩니다.

*   **브랜치 생성과 동시에 전환:**
    ```bash
    git checkout -b feature/login-new
    # 또는
    git switch -c feature/login-new
    ```

#### 4.3 브랜치 목록 확인

```bash
git branch        # 로컬 브랜치 목록 확인 (현재 브랜치는 * 표시)
git branch -a     # 로컬 및 원격 브랜치 모두 확인
```

#### 4.4 브랜치 병합 (`git merge`)

다른 브랜치의 변경 사항을 현재 브랜치로 가져와 통합합니다.

1.  **병합할 브랜치로 전환:**
    ```bash
    git checkout main # feature/login 브랜치를 main으로 병합하고 싶다면 main 브랜치로 이동
    ```
2.  **병합 실행:**
    ```bash
    git merge feature/login # feature/login 브랜치의 변경 사항을 현재 (main) 브랜치로 병합
    ```
*   **Fast-forward Merge:** 병합하려는 브랜치가 현재 브랜치보다 앞서 나간 경우, 단순히 HEAD 포인터만 이동시켜 병합합니다. 별도의 병합 커밋이 생성되지 않습니다.
*   **3-way Merge (Recursive Merge):** 두 브랜치가 공통 조상 커밋 이후 각자 다른 커밋을 가지고 있을 때, Git이 두 브랜치의 변경 사항을 합쳐 새로운 병합 커밋을 만듭니다.

#### 4.5 병합 충돌 (Merge Conflict) 해결

두 브랜치에서 같은 파일의 같은 부분을 서로 다르게 변경했을 때 발생합니다.

1.  **충돌 발생 시:** `git status`를 실행하면 충돌이 발생한 파일들을 알려줍니다.
    ```
    Unmerged paths:
      (use "git add <file>..." to mark resolution)
        both modified: index.html
    ```
2.  **충돌 파일 확인:** 충돌이 발생한 파일을 텍스트 에디터로 엽니다. Git이 충돌 부분을 특수 마커로 표시합니다.
    ```html
    <<<<<<< HEAD
    <p>이것은 현재 브랜치(HEAD)의 내용입니다.</p>
    =======
    <p>이것은 병합하려는 브랜치(feature/login)의 내용입니다.</p>
    >>>>>>> feature/login
    ```
3.  **수동 해결:** `<<<<<<<`, `=======`, `>>>>>>>` 마커를 제거하고 원하는 최종 코드로 수정합니다.
4.  **해결된 파일 스테이징:**
    ```bash
    git add index.html # 충돌 해결 후 Git에 알림
    ```
5.  **병합 커밋 완료:**
    ```bash
    git commit # Git이 자동으로 병합 커밋 메시지를 생성합니다. 그대로 저장하거나 수정합니다.
    ```
*   **팁:** VS Code와 같은 에디터는 Git 충돌 해결 기능을 내장하고 있어 시각적으로 편리하게 해결할 수 있습니다.

#### 4.6 브랜치 삭제 (`git branch -d`)

병합이 완료되어 더 이상 필요 없는 브랜치를 삭제합니다.

```bash
git branch -d feature/login # 병합된 브랜치만 삭제 가능
git branch -D old-branch   # 강제 삭제 (병합되지 않은 내용이 있어도 삭제, 주의!)
```

---

### 5. 원격 저장소(Remote Repository) 연동

로컬 저장소의 변경 사항을 원격 저장소와 동기화합니다.

#### 5.1 원격 저장소 확인 (`git remote`)

현재 저장소가 연결된 원격 저장소 목록을 확인합니다.

```bash
git remote       # 원격 저장소 이름 목록 (기본값은 'origin')
git remote -v    # 원격 저장소 이름과 URL 함께 확인
```

#### 5.2 원격 저장소 추가/제거 (`git remote add/remove`)

*   **추가:**
    ```bash
    git remote add origin https://github.com/username/repository-name.git
    # 'origin'은 원격 저장소의 별명입니다. 일반적으로 'origin'을 사용합니다.
    ```
*   **제거:**
    ```bash
    git remote remove origin
    ```

#### 5.3 원격 저장소의 변경 사항 가져오기 (`git fetch`)

원격 저장소의 최신 변경 사항을 로컬로 가져오지만, 현재 작업 브랜치에는 병합하지 않습니다. 원격 브랜치(`origin/main` 등)를 업데이트합니다.

```bash
git fetch origin # 'origin' 원격 저장소의 모든 브랜치 변경 사항 가져오기
git fetch origin main # 'origin'의 main 브랜치 변경 사항만 가져오기
```
*   `git log origin/main` 등으로 원격 브랜치 내용을 확인할 수 있습니다.

#### 5.4 로컬 저장소 업데이트 (`git pull`)

원격 저장소의 변경 사항을 가져와(fetch) 현재 로컬 브랜치에 자동으로 병합(merge)합니다.

```bash
git pull origin main # 'origin' 원격 저장소의 'main' 브랜치 변경 사항을 가져와 현재 로컬 브랜치에 병합
```
*   자주 사용하는 명령어이며, 협업 시에는 `git push` 전에 `git pull`을 먼저 실행하여 최신 상태를 유지하는 것이 좋습니다.

#### 5.5 로컬 변경 사항 원격 저장소에 반영 (`git push`)

로컬 저장소의 커밋들을 원격 저장소에 업로드합니다.

```bash
git push origin main # 로컬 'main' 브랜치의 변경 사항을 'origin' 원격 저장소의 'main' 브랜치로 업로드

# 새 브랜치를 원격 저장소에 처음 푸시할 때
git push -u origin feature/new-feature
# '-u' 또는 '--set-upstream' 옵션을 사용하면 이후부터는 'git push'만으로 해당 브랜치가 추적됩니다.
```
*   **주의:** 다른 사람이 먼저 푸시한 내용이 있다면 `git push`가 거부될 수 있습니다. 이 경우 먼저 `git pull`하여 최신 상태를 반영한 후 다시 푸시해야 합니다.
*   **`--force` 사용 주의:** `git push --force`는 원격 저장소의 히스토리를 강제로 덮어씁니다. 협업 환경에서는 절대 사용하지 않아야 합니다. (Rebase 후 자신의 로컬 브랜치 푸시 시 등 특정 상황에서만 사용)

#### 5.6 SSH 키 설정 (선택 사항, 권장)

매번 사용자 이름과 비밀번호를 입력하는 대신 SSH 키를 사용하여 원격 저장소에 접근할 수 있습니다.

1.  **SSH 키 생성:**
    ```bash
    ssh-keygen -t ed25519 -C "당신의 이메일@example.com"
    ```
    *   `Enter file in which to save the key (...):` 프롬프트에서 기본 경로(`C:\Users\YourUser\.ssh\id_ed25519`)를 사용하거나 원하는 경로를 지정합니다.
    *   패스프레이즈(비밀번호)를 설정할 수 있습니다.
2.  **SSH 에이전트 시작:**
    *   Windows 10에서는 `ssh-agent`가 기본적으로 백그라운드에서 실행될 수 있습니다.
    *   Powershell에서 다음 명령어로 확인하거나 시작할 수 있습니다:
        ```powershell
        Get-Service ssh-agent
        Start-Service ssh-agent # If not running
        ```
3.  **SSH 키 추가:**
    ```bash
    ssh-add ~/.ssh/id_ed25519
    ```
4.  **공개 키 복사:** `C:\Users\YourUser\.ssh\id_ed25519.pub` 파일을 텍스트 에디터로 열어 내용을 복사합니다.
5.  **GitHub/GitLab/Bitbucket에 등록:** 해당 플랫폼의 'Settings' -> 'SSH and GPG keys' (또는 유사한 메뉴)에 복사한 공개 키를 추가합니다.
6.  **원격 URL 변경:** 기존 `https` URL 대신 `ssh` URL을 사용하도록 원격 저장소 URL을 변경합니다.
    ```bash
    git remote set-url origin git@github.com:username/repository-name.git
    ```

---

### 6. 작업 되돌리기 (Undo Changes)

Git의 강력한 기능 중 하나로, 실수했을 때 또는 작업 내용을 되돌리고 싶을 때 유용합니다.

#### 6.1 작업 디렉토리 변경 취소 (`git restore`)

아직 스테이징되지 않은(untracked 또는 modified) 파일의 변경 사항을 되돌립니다.

```bash
# 특정 파일의 변경 사항을 HEAD(마지막 커밋) 상태로 되돌림
git restore index.html

# 현재 작업 디렉토리의 모든 변경 사항을 되돌림 (주의!)
git restore .
```

#### 6.2 스테이징 영역 변경 취소 (`git restore --staged`)

`git add`로 스테이징했던 파일을 스테이징 영역에서 다시 작업 디렉토리로 내립니다.

```bash
git restore --staged index.html
# 또는 (구버전에서 주로 사용)
git reset HEAD index.html
```
*   파일 내용은 변하지 않고, 단지 스테이징 상태만 해제됩니다.

#### 6.3 커밋 되돌리기 (`git reset`)

과거의 특정 커밋으로 HEAD 포인터를 이동시킵니다. 커밋 히스토리를 재작성하는 강력한 명령어이므로 사용에 주의가 필요합니다.

```bash
# --soft: HEAD를 특정 커밋으로 이동시키지만, 스테이징 영역과 작업 디렉토리 내용은 그대로 둠.
#         이전 커밋들은 사라지지만 변경 내용은 스테이징된 상태로 유지.
git reset --soft HEAD~1 # 바로 이전 커밋으로 되돌림
git reset --soft <commit-hash>

# --mixed (기본값): HEAD와 스테이징 영역을 특정 커밋으로 이동시키지만, 작업 디렉토리 내용은 그대로 둠.
#                   이전 커밋들은 사라지고, 변경 내용은 스테이징되지 않은 상태로 작업 디렉토리에 남음.
git reset --mixed HEAD~1 # 'git reset HEAD~1' 과 동일
git reset <commit-hash>

# --hard: HEAD, 스테이징 영역, 작업 디렉토리 모두 특정 커밋으로 이동시키고 모든 변경 사항을 버림.
#         실수하면 작업 내용이 완전히 사라지므로 **매우 주의**해야 함.
git reset --hard HEAD~1 # 바로 이전 커밋으로 완전히 되돌림
git reset --hard <commit-hash>
```
*   `HEAD~1`: 현재 HEAD에서 한 단계 이전 커밋을 의미합니다. `HEAD~2`는 두 단계 이전입니다.

#### 6.4 커밋 내용 수정 (`git commit --amend`)

가장 최근 커밋의 메시지를 수정하거나, 스테이징된 새로운 변경 사항을 이전 커밋에 추가합니다.

```bash
# 마지막 커밋 메시지 수정
git commit --amend

# 마지막 커밋에 새로운 변경 사항 추가
# 1. 파일 수정 및 스테이징
git add new_changes.js
# 2. --amend로 이전 커밋에 통합
git commit --amend --no-edit # 메시지 변경 없이 변경 사항만 추가
```
*   **주의:** 이미 원격 저장소에 푸시된 커밋을 `--amend`로 수정하면, 히스토리가 재작성되므로 협업에 문제가 생길 수 있습니다. 푸시 전의 커밋에만 사용하는 것이 좋습니다.

#### 6.5 특정 커밋 취소 (`git revert`)

과거의 특정 커밋에서 발생한 변경 사항을 되돌리는 새로운 커밋을 만듭니다. `git reset`과 달리 히스토리를 건드리지 않고, 새로운 커밋으로 되돌리기 때문에 협업 환경에서 안전하게 사용할 수 있습니다.

```bash
git revert <commit-hash> # 해당 커밋의 변경 사항을 되돌리는 새로운 커밋 생성
```

#### 6.6 작업 임시 저장 (`git stash`)

현재 작업 중인 변경 사항을 임시로 저장하여 다른 브랜치로 전환하거나 다른 작업을 할 수 있도록 합니다. (커밋할 준비가 안 되었지만 저장하고 싶은 경우)

```bash
git stash save "작업 중이던 기능 임시 저장" # 현재 작업 내용 임시 저장
git stash list                        # 저장된 stash 목록 확인
git stash apply                       # 가장 최근 stash 적용 (stash는 남음)
git stash pop                         # 가장 최근 stash 적용 후 삭제
git stash drop                        # 가장 최근 stash 삭제
git stash clear                       # 모든 stash 삭제
```

---

### 7. 고급 Git 활용 (Rebase, Tag)

#### 7.1 리베이스(Rebase): 히스토리 정렬 (`git rebase`)

브랜치의 커밋 히스토리를 재작성하여 더 깔끔하고 선형적인 히스토리를 만듭니다.

```bash
# 현재 브랜치를 'main' 브랜치 위에 리베이스
git rebase main
```
*   **작동 방식:** Git은 현재 브랜치(feature)의 변경 사항을 `main` 브랜치의 최신 커밋 위에 "재적용"합니다. 이렇게 하면 `feature` 브랜치의 모든 커밋이 `main` 브랜치의 최신 커밋 이후에 나타나게 되어 마치 `main`에서 시작한 것처럼 보입니다.
*   **대화형 리베이스 (Interactive Rebase):**
    ```bash
    git rebase -i HEAD~3 # 최근 3개 커밋을 대화형으로 리베이스
    ```
    *   커밋들을 합치기(squash), 메시지 변경(reword), 순서 변경(reorder), 삭제(drop) 등 다양한 작업을 할 수 있습니다.
*   **주의사항:**
    *   **공유된 브랜치에서는 절대로 `rebase`를 사용하지 마십시오.** `rebase`는 커밋 히스토리를 재작성하므로, 이미 다른 사람과 공유된 커밋을 `rebase`하면 협업자들에게 큰 혼란을 야기하고 히스토리가 꼬일 수 있습니다.
    *   `rebase`는 자신의 로컬 브랜치에서 아직 푸시하지 않은 커밋들을 정리할 때 주로 사용합니다.

#### 7.2 태그(Tag): 중요 시점 표시 (`git tag`)

특정 커밋에 영구적인 "별명"을 붙여 중요 릴리즈 버전 등을 표시할 때 사용합니다.

```bash
# 가벼운 태그 (Lightweight Tag): 단순히 특정 커밋에 대한 포인터
git tag v1.0

# 주석이 달린 태그 (Annotated Tag): 태그 생성자, 날짜, 메시지 등 추가 정보 포함 (권장)
git tag -a v1.0 -m "Release version 1.0"

# 특정 커밋에 태그 달기
git tag -a v1.0.1 <commit-hash> -m "Bugfix release"

# 태그 목록 확인
git tag

# 태그를 원격 저장소에 푸시 (태그는 기본적으로 푸시되지 않음)
git push origin v1.0
git push origin --tags # 모든 태그 푸시

# 태그 삭제
git tag -d v1.0            # 로컬 태그 삭제
git push origin :refs/tags/v1.0 # 원격 태그 삭제
```

---

### 8. Git GUI 도구 (선택 사항)

명령줄(CLI)에 익숙하지 않거나 시각적인 관리를 선호한다면 GUI 도구를 활용할 수 있습니다.

*   **Git GUI:** Git 설치 시 함께 제공되는 기본 GUI 도구.
*   **Sourcetree:** Atlassian에서 제공하는 강력하고 인기 있는 Git GUI 클라이언트.
*   **GitKraken:** 깔끔하고 직관적인 UI가 특징인 Git 클라이언트.
*   **Visual Studio Code:** 내장된 Git 연동 기능이 매우 강력하여 대부분의 Git 작업을 에디터 내에서 처리할 수 있습니다. (확장 프로그램 설치 필요 없음)
*   **GitHub Desktop:** GitHub 사용자를 위한 간단하고 편리한 GUI 도구.

---

### 9. 문제 해결 및 팁

#### 9.1 자주 발생하는 문제

*   **`git pull` 또는 `git push` 시 "Updates were rejected because the remote contains work that you do not have locally" 오류:**
    *   원격 저장소에 내가 로컬에 없는 최신 변경 사항이 있는 경우 발생합니다.
    *   **해결:** 먼저 `git pull`을 실행하여 로컬 저장소를 최신 상태로 업데이트하고, 필요한 경우 충돌을 해결한 후 다시 `git push` 합니다.

*   **커밋 메시지 에디터가 Vim으로 열림:**
    *   Git 설치 시 기본 에디터를 Vim으로 설정했거나, `core.editor` 설정이 없는 경우 발생합니다.
    *   **해결:** `1.3 기본 텍스트 에디터 설정` 섹션을 참고하여 선호하는 에디터로 변경합니다. Vim에서 빠져나가려면 `Esc` 키를 누른 후 `:wq` (저장 후 종료) 또는 `:q!` (저장하지 않고 종료)를 입력하고 Enter를 누릅니다.

*   **`git commit --amend` 후 `git push` 시 오류:**
    *   `--amend`는 커밋 히스토리를 재작성하므로, 이미 원격에 푸시된 커밋을 수정하면 로컬 히스토리와 원격 히스토리가 달라져 발생합니다.
    *   **해결:** 개인 브랜치에서 아직 아무도 풀(pull)하지 않았고 히스토리 재작성이 괜찮다면 `git push --force` (또는 `--force-with-lease`)를 사용할 수 있습니다. **하지만 공유 브랜치에서는 절대 사용하지 마십시오.** 대신 `git revert`를 사용하여 안전하게 변경 사항을 되돌리는 것이 좋습니다.

#### 9.2 유용한 Git 명령어 별칭(Alias) 설정

자주 사용하는 긴 명령어를 짧은 별칭으로 설정하여 편리하게 사용할 수 있습니다.

```bash
git config --global alias.co checkout     # git co 로 git checkout 사용
git config --global alias.br branch       # git br 로 git branch 사용
git config --global alias.ci commit       # git ci 로 git commit 사용
git config --global alias.st status       # git st 로 git status 사용
git config --global alias.hist "log --oneline --graph --decorate" # git hist 로 예쁜 로그 확인
```

#### 9.3 좋은 커밋 메시지 작성법

*   **첫 줄은 간결하게 요약:** 변경 내용의 핵심을 50자 이내로 작성합니다. (예: `feat: 로그인 기능 구현` 또는 `fix: 회원가입 버그 수정`)
*   **두 번째 줄은 비워둠:** 첫 줄과 본문 사이를 구분합니다.
*   **본문은 상세 설명:** 변경 내용, 배경, 문제점, 해결 방법 등을 구체적으로 설명합니다.
*   **명령형 어조 사용:** "Add feature" (기능 추가), "Fix bug" (버그 수정) 같이 명령형으로 작성합니다.
*   **영어 사용 (선택 사항):** 글로벌 협업을 염두에 둔다면 영어로 작성하는 것이 좋습니다.

---

이 매뉴얼이 Windows 10 환경에서 Git을 효과적으로 활용하는 데 도움이 되기를 바랍니다. Git은 꾸준히 연습하고 직접 부딪혀보면서 실력이 향상됩니다. 궁금한 점은 언제든 Git 공식 문서나 온라인 자료를 참고하십시오.