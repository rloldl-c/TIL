# Branch
커밋 흐름의 가지치기<br>
각자 독립된 버전의 흐름을 만들 수 있다
=> 협업을 위해 독립적인 흐름을 만드는 것
## branch
- 독립적인 작업흐름을 만들고 관리
### 브랜치 주요 명령어
1. 생성

    ```bash
    $ git branch {branch name}
    ```

2. 이동
    ```bash
    $ git checkout {branch name}
    ```
3. 생성 및 이동
    ```bash
    $ git checkout -b {branch name}
    ```
4. 삭제
    ```bash
    $ git branch -d {branch name}
    ```
5. 목록 확인
    ```bash
    $ git branch
    ```
6. 병합
    ```bash
    $ git merge {branch name}
    ```
  - 현재 작성중인 브랜치에 {branch name}이 병합

## brach 활용 시나리오
### 상황 1. fast-forward
> 새로운 브랜치 생성 후 master 브랜치에 변경 사항이 없는 상황
1. feature/home branch 생성 및 이동
    ```bash
    $ git checkout -b feature/home
    ```

2. 작업 완료 후 commit
    ```bash
    (feature/home) $ touch home.txt
    (feature/home) $ git add .
    (feature/home) $ git commit -m 'Add home.txt'
    ```

3. master 이동
    ```bash
    (feature/home) $ git checkout master
    ```

4. master에 병합
   ```bash
   (master) $ git merge feature/home
   ```
   ```bash
   Updating e89616a..b534a34
   Fast-forward
    home.txt | 0
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 home.txt
   ```

5. 결과 : fast-foward
    ```bash
   (master) $ git log --oneline
   b534a34 (HEAD -> master, feature/home) Complete Home!!!!
   e89616a Init
   ```

6. branch 삭제
   ```bash
   (master) $ git branch -d feature/home
   ```


### 상황 2. merge commit
> 다른 파일이 수정된 커밋을 병합하는 상황
>
> git이 자동으로 merge 진행

1. feature/about branch 생성 및 이동
   ```bash
   (master) $ git checkout -b feature/abou
   ```

2. 작업 완료 후 commit
   ```bash
   (feature/about) $ touch about.txt
   (feature/about) $ git add .
   (feature/about) $ git commit -m 'Add about.txt'
   ```

3. master 이동
   ```bash
   (feature/abou) $ git checkout master
   ```

4. **master에 추가 commit 이 발생시키기!!**
   * 다른 파일을 수정하는 경우

   ```bash
   (master) $ touch master.txt
   (master) $ git add .
   (master) $ git commit -m 'Add master.txt'
   ```

5. master에 병합
   ```bash
   (master) $ git merge feature/aout
   ```

6. 결과 -> 자동으로 *merge commit 발생*
   * vim 편집기 화면이 나타납니다. 

     * 자동으로 작성된 커밋 메시지를 확인하고, `esc`를 누른 후 `:wq`를 입력하여 저장 및 종료를 합니다.
       * `w` : write
       * `q` : quit

7. 커밋 및 그래프 확인하기
   ```bash
   $ git log --onelie --graph
   ```
   ```bash
   $ git log --oneline --graph
   *   582902d (HEAD -> master) Merge branch 'feature/about'
   |\
   | * 5e1f6de (feature/about) 자기소개 페이지 완료!
   * | 98c5528 마스터 작업....
   |/
   * b534a34 Complete Home!!!!
   * e89616a Init
   ```

8. branch 삭제
   ```bash
   (master) $ git branch -d feature/about
   ```


### 상황 3. merge commit 충돌
> 같은 파일이 수정된 커밋을 병합하는 상황
>
> git이 자동으로 merge하지 못하여 직접 수정해야 함

1. feature/test branch 생성 및 이동
   ```bash
   (master) $ git checkout -b feature/test
   ```

2. 작업 완료 후 commit
   ```bash
   # README.md 파일 열어서 수정
   (feature/test) $ touch test.txt
   (feature/test) $ git add .
   (feature/test) $ git commit -m 'Add test.txt'
   ```

3. master 이동
   ```bash
   (feature/test) $ git checkout master
   ```

4. **master에 추가 commit 이 발생시키기!!**
   * 동일 파일을 수정 혹은 생성하는 상황

   ```bash
   # README.md 파일 열어서 수정
   (master) $ git add README.md
   (master) $ git commit -m 'Update README.md'
   ```

5. master에 병합
   ```bash
   (master) $ git merge feture/test
   ```
   ```bash
   Auto-merging README.md
   CONFLICT (content): Merge conflict in README.md
   Automatic merge failed; fix conflicts and then commit the result.
   ```

6. 결과 -> *merge conflict발생*
   > git status 명령어로 충돌 파일을 확인할 수 있음.
   ```bash
   (master|MERGING) $ git status
   On branch master
   You have unmerged paths.
     (fix conflicts and run "git commit")        
     (use "git merge --abort" to abort the merge)
   
   Changes to be committed:
           new file:   test-1.txt
           new file:   test-2.txt
           new file:   test.txt
   
   Unmerged paths:
     (use "git add <file>..." to mark resolution)
           both modified:   README.md
   ```

7. 충돌 확인 및 해결
   ```
   <<<<<<< HEAD
   # 마스터에서 작업함...
   =======
   # 테스트에서 작성
   >>>>>>> feature/test
   ```

8. merge commit 진행

   ```bash
   (master|MERGING) $ git add.
   (master|MERGING) $ git commit
   ```

   * vim 편집기 화면이 나타납니다.

     * 자동으로 작성된 커밋 메시지를 확인하고, `esc`를 누른 후 `:wq`를 입력하여 저장 및 종료를 합니다.
     * `w` : write
     * `q` : quit

9. 커밋 및 확인하기
   ```bash
   (master) $ git log --oneline --graph
   *   bc1c0cd (HEAD -> master) Merge branch 'feature/test'
   |\  
   | * 95fad1c (feature/test) README 수정하고 test 작성하고
   * | 2ecad28 리드미 수정
   |/  
   *   582902d Merge branch 'feature/about'
   |\  
   | * 5e1f6de 자기소개 페이지 완료!
   * | 98c5528 마스터 작업....
   |/  
   * b534a34 Complete Home!!!!
   * e89616a Init
   ```

10. branch 삭제
    ```bash
    (master) $ git branch -d feature/test
    ```


# GitHub Flow
## 로컬에서 병합하는 게 아니라 브랜치로 push한 다음 pull request 생성 후 병합
```bash
$ git push origin master (X)
$ git push origin branch_name (O)
```
- 때문에 작업을 이어하기 위해서는 $ git pull을 먼저 수행해야 함
