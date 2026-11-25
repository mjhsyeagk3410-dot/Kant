# 2026-10-27 TIL

## rm 의 쓰임새
```sh
git rm -rf
```
- rm은 삭제다 문제는 되살릴수없다 복구가 되도 완벽하지 않고 돈이 많이 든다.
- rm은 근데 만약 다른 프로그램으로 실행하고 있을땐, 삭제가 안된다. 
- 근데 rm만 쓰는경우는 잘 없고 rm -rf 를 한 세트로 기억해야 좋다 

오늘도 알아보는 마크다운 문법
- -r : 리커시브
- f : 포스(묻지않고 강제삭제)

```sh
rm -rf . 
```
- 위 기능은 시스템을 전부 초기화한다. 지금은 안전장치로 인해서 안된다고 나온다

## 마크다운문법 / #의 쓰임새
```md
# 제목1
## 제목2
### 제목3
```

- 이후 띄어쓰기를 해야 다음 문자가 마크다운으로 인식됨 

```sh
echo "# Markdown Tutorial" > README.md
```
- 바로 파일을 만들고 그 안에 텍스트를 저장할때. 그리고 #은 제목을 의미함. 
- vs code 에서 터미널을 여는 방법, 파워셀을 bash로 바꾸는 방법 
- vs code 에서 터미널을 똑같이 사용이 가능함. 
- ctrl+l(엘) 을 누르면 히스토리에서 모든 명령어 기록을 다 지움. 

- 설치된 소프트웨어중 git bash라는 별도의 터미널도 있음. 
(검색에서 그냥 git치면 나옴)

```sh
git --version
```
위 코드는 깃 버전을 확인할때 쓴다 

```sh
git config --list
```
깃이 설정된 설정값을 보는 옵션을 볼때 씀 
```sh
git config --global user.email "e-mail"
```
이건 왜? 
- 깃허브는 협업도구인데 나중에 협업할때 뭐 이메일같은거라던지 알기위해 
그것을 초기에 세팅한다. 

오탈자가 생겼다? 
```sh
git config --global --unset user.email "e-mail"
```
--unset 을 유저이메일 앞에 삽입. 그러면 지워진다.
```sh 
git config --global user.name "SeoJaeHong"
```
이메일만 보면 모르니까 이름도 적는 작업
### 이것은 깃 쓸때 맨처음에만 설정해주면 된다. 

잘됐나 확인하고 싶다?
```sh
git config --list 
```
위 코드를 쳐서 확인. 

---

```sh
git init
```
깃 폴더 초기화
- 치면 나오는 값: Initialized empty Git repository in C:/Users/USER/kant/.git/
- 보통 _kant git main 이라고 뜨기도 함. 

```sh
cd .git
```
.git로 이동. (폴더에서는 확인안됨)

```sh
git status
``` 
- notion to commit은 아직 커밋을 안했다는 뜻
- untracked는 아직 추적 관리하고있지않다는 뜻 (파일 옆에 U라는 모양) 
- 이때 git add를 하라고 가이드를 해준다. 

```sh
git add README.md
```
- 이러면 이제 파일 옆에 A라고 바껴있다 (add를했다는 뜻) M은 저장된것. 
- 이제 스테이터스 치면 빨간색이였던게 지금은 녹색으로 되어있다.
(스테이징으로 들어갔을때만 뜸.)

커밋을 해보자:
```sh 
git commit -m "feat: Add README.md"
``` 

위에것을 치면 나오는것:
```md
 [main (root-commit) 783e7d1] feat: Add README.md
 1 file changed(파일하나 바뀜), 1 insertion(+)(추가된것)
 create mode 100644 README.md
 ```

커밋을 확인해보자: 
```sh
git log
```

치면?
```md 
commit 783e7d19587a4f8711ddff28f8181751e9f5264f (HEAD -> main)
Author: SeoJaeHong <mjhsyeagk3410@gmail.com>
Date:   Tue Oct 27 10:20:57 2026 +0900

    feat: Add README.md
```
이렇게 누가 무슨 커밋을했고 이 커밋을 누가 했는지가 다 뜬다. 

터미널을 쓰다가 (end)가 나올때가 있다. 이때 Q를 눌러라.  

틸드 세개 치는 경우: 

```md
# 헤더1
## 헤더2
### 헤더3
```
위와 같이 코드모양으로 만들때 사용이 된다. 

오늘의 단축키
ctrl + shigt + v : 웹브라우저에서 어떻게 보이는지 보임(마크다운 프리뷰로 바뀜 평소에는 텍스트 에디터) 또 단축키 누르면 텍스트 에디터로 돌아감. 

보통 add를 할때 그 파일 이름으로 적어도 되지만, 만약 하나밖에 없다면 add . 을 하면 된다. 

- 커밋을 할때 -m을 안치면 뭔가 이상하게 뜨는 상황에서, 일단 I(아이)눌러라 그리고 맨 위에 docs라고 치고 콜론 치고 헤더내용추가를 친다. 
- 그리고 esc를 누르고, 쉬프트+콜론을 누르면 입력을 할수 있다. 그리고 w를 먼저 친다. w는 저장이다. q는 나온다는 뜻 합쳐서 저장하고 나온다는 뜻 
- 이러면 이 창이 나가진다. (저장을 안하고 나오면 커밋이 안된다. 저장하고 나오면 커밋이 된다) 

---
```sh
git log --oneline
```
위와 같이 치면 필요한 정보만 출력됨. 
 
```md
1350437 (HEAD -> main) feat: 뷸렛 사용법 추가
247ca78 docs: 헤더 내용 추가
783e7d1 feat: Add README.md
```
위에 왼쪽에 입력된 값은 커밋을 한 버전의 약자 . 

- 깃 리셋, 깃 리버브?스?를 안치고 그 전으로 돌아가고 싶을때? 
- 일단 몇칸 뒤로 갈건지? 만약 30개가 있을때 특정 칸으로 다이렉트로 갈건지?

```sh
git checkout
```
위와 같이 치면 가고싶은 특정 커밋으로 이동할때 쓴다. (git log --oneline을 이용하면 그 점프하고싶은 곳으로 가기 편한 값이 나오는데 그걸 복사하고 체크아웃 뒤에 붙여넣기하면됨) 이후 git log를 하면, 두개밖에 안뜬다. 헤드 이전것이 안보임. 

```sh
git log --oneline --all
```
위와같이 치면 다 뜬다. 

### 주의사항: 긴 작업을할때 (마크다운안의) 내용이 수정이 되었는지 봐야한다. 수정이 되면 안된다. 