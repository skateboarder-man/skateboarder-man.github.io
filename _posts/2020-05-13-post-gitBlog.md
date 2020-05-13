---
title: "그대로 따라하면 되는 Git Blog 만들기"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Post Formats
  - readability
  - standard
---

# 1. Ruby 설치
   - 공식 홈페이지에서 다운받아 편하게 설치한다.
   - <https://rubyinstaller.org/>
   - 설치후 command 창을 열고 아래와 같이 입력한다. (버전 확인)
   ```yaml
   ruby -v
   ```
   

# 2. Git Bash 설치
   - GitHub 사용이 필요 하기 때문에 설치 한다.
   - <https://git-scm.com/downloads>
   - 설치옵션은 사용자에 맞게 선택하여 설치해준다.

# 3. GitHub 블로그 생성
   - 회원가입 한다.
   - Repositories 생성 한다.
   - Repository name 을 사용자아이디.github.io 입력
   - Public 선택
   - Initialize this repository with a README 체크박스 체크
   - Create repositoty 클릭
   -  https://사용자아이디.github.io 접속하여 화면에 사용자아이디.github.io 나오면 성공

# 4. jekyllthemes 선택
   - <https://jekyllthemes.io> 접속
   - 원하는 형태의 theme 선택
   - 필자는 <https://mmistakes.github.io/minimal-mistakes/> 사용하였다.
   - <https://github.com/mmistakes/mm-github-pages-starter/generate> 클릭시 바로 Repository 생성 페이지로 이동한다.
   - Repository 생성하면 바로 theme 을 받아온다.
   - 받아오기 완료 하면 다시 https://사용자아이디.github.io 접속하여 화면에 블로그가 나오는지 확인.
   - 블로그 나오면 선택한 theme을 자기 자신의 블로그에 올린것이다.

# 5. GitHub Clone 하기
   - git 홈피에서 자신의 Repository의 주소를 복사한다. (Clone and Download를 클릭하면 된다.)
   - 탐색기를 열고 원하는 위치에 Directory 생성 한다.
   - command 창을 열고 다음과 같이 입력한다.
   ```yaml
   cd <Directory 생성 위치>
   ```
   예)cd Portpolio<폴더명>
  
   ```yaml
   git clone [복사한 주소]
   ```
   예) get clone https://github.com/사용자아이디/사용자아이디.github.io.git
   - Git에 올린 파일에 복사되어 자신의 폴더에 들어가게 된다.

# 6. gem 설치하기
  - command를 이용하여 복사된 파일이 있는 Directord 들어가 gem 설치
  - 아래와 같이 입력한다.
  ```yaml
   cd 사용자아이디.github.io
   gem install bundler
   bundle install
   ```

# 7. jekyll bundler 설치
  - 블로그 수정 사항 바로바로 확인 할수있는 방법이다.
  - command 창에 아래와 같이 입력한다.

   ```yaml
   gem install jekyll bundler
   cd [Git Clone (Directory) 입력] 
   bundle exec jekyll serve
  
   ```

   - localhost:4000 확인후 인터넷 주소창에 입력 하면 블로그 화면을 볼수 있다.

# 8. Visual Studio Code 설치
   - 설치후 git Clone directory를 찾아 열어 주면 수정할수 있다.
   - _posts 폴더 안의 XXX.md 파일을 복붙하여 똑같은 형식으로 만들어 주면 된다.
   - _config.yml 파일에 # Site settings 부분에 아래와 같이 추가해 준다.

url: "https://사용자아이디.github.io"
baseurl: # the subpath of your site, e.g. "/blog"
github_username: github 사용자 아이디
minimal_mistakes_skin: default
search: true

   - navigation.yml 수정하면 메뉴바 수정이 가능하다.
   - _pages 폴더에 xxx.md 파일을 만들어 메뉴바에 입력한 링크를 연결시켜 작성하고 싶은 내용 입력하면 된다.