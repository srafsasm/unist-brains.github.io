[![Build Status](https://app.travis-ci.com/UNIST-brAIns/unist-brains.github.io.svg?branch=master)](https://app.travis-ci.com/UNIST-brAIns/unist-brains.github.io)

# brAIns Blog

Blog of UNIST AI club, brAIns

[Link](https://unist-brains.github.io/)

# 블로그 작성과 코드 업로드 방법을 소개합니다!

작성자: 정용준

brAIns 동아리 활동을 진행하면서 블로그 포스팅을 하거나 스터디 내에서 코드를 공유하는 일이 많이 있을 텐데요, 이 글은 어떻게 글을 포스팅하거나 코드를 업로딩하는지에 대해 설명드리고자 작성되었습니다! git commit,push를 통해 이를 진행하게 되는데, 시작하기 전에 몇 가지 준비 과정이 필요합니다.

# 1. 준비 과정

먼저 간단히 설명드리면, brAIns 블로그와 코드 공유의 경우 github organization을 통해 운영되기 때문에, 컴퓨터에 git과 text editor가 설치되어 있어야 합니다.

* git 설치하기
* github 계정 생성하기
* text editor 설치하기

git 설치 방법은 Window, Mac, Linux 등 운영체제에 따라 방식이 상이하여 이 글에서 직접 다루지는 않지만, 인터넷에 "(운영체제) git 설치" 와 같이 검색하시면 자세히 다루는 글들을 쉽게 찾아보실 수 있습니다. git 설치 이후 사용자 닉네임과 이메일을 등록하는 과정까지 진행해 주시면 충분합니다.   

github 계정은 없으신 경우 [github 사이트](https://github.com/)에서 만드실 수 있습니다.   

text editor의 경우에는 종류는 무관하며, 아직 사용하고 있지 않으시다면 개인적으로는 [VS Code](https://code.visualstudio.com/)를 추천드립니다!   

세 가지가 모두 준비되었다면 본격적으로 초기 설정을 진행해보도록 하겠습니다. (Windows환경, VS Code 사용 기반 설명으로, 환경과 text editor 종류에 따라 사진과 완전히 동일하지 않을 수 있습니다!)
   

# 2. 초기 설정

블로그 포스팅과 코드 업로드는 기본적으로 로컬 디렉토리에 로컬 저장소를 만들어 brAIns 데이터베이스의 원격 저장소와 연동하고, 연동된 로컬 저장소에서 branch를 만들어 수정한 뒤 brAIns 데이터베이스에 commit,push를 통해 업로드하는 방식으로 이루어집니다. (보다 자세한 원리가 궁금하신 분들은 [git의 원리](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC%EB%9E%80%3F)를 더 읽어 보시면 좋을 것 같습니다.)   

초기 설정은 바로 로컬 저장소를 새로 만들고, 원격 저장소와 연동하는 과정을 진행하는 것이라고 보시면 될 것 같습니다.   

먼저 원하는 위치에 새 폴더를 생성합니다. 이 폴더에 로컬 저장소를 생성하도록 하겠습니다. [github](https://github.com/)에 접속하여 로그인한 뒤, [unist brAIns github 페이지](https://github.com/UNIST-brAIns/unist-brains.github.io)에 접속하여 우측 상단의 "Fork" 버튼을 눌러 자신의 github repository에 brAIns repository를 복사해 옵니다.

![fork butten](../assets/images/Capture0322/capture1.jpg)

복사된 repository에 들어가 우측 상단의 "Code" 버튼을 눌러줍니다. 새로 뜬 창에서 HTTPS 주소를 복사 버튼을 눌러 복사해줍니다. 

![repository](../assets/images/Capture0322/capture2.jpg)

이후 새로 생성한 폴더에서 우클릭을 통해 git bash를 열어 git command 창을 띄워줍니다(Mac의 경우 terminal). 열린 command 창에 다음 코드를 입력하여 로컬 디렉토리를 fork해온 unist brAIns 저장소와 연동해줍니다.(복사한 주소) 위치에 (git bash의 경우) shift+insert를 통해 복사한 주소를 입력해줍니다. (괄호는 없어야 합니다!)

    git clone (복사한 주소)

이렇게 하면, unist brAIns 저장소에 존재하는 모든 파일들이 다음과 같이 새로 만든 폴더에 복사되어 들어온 것을 볼 수 있습니다.

![cloned folder](../assets/images/Capture0322/capture3.jpg)

이제 로컬 저장소를 brAIns 원격 저장소와 연동해주기 위해 다시 [unist brAIns github 페이지](https://github.com/UNIST-brAIns/unist-brains.github.io)에 접속합니다. 이번에는 fork해온 자신의 repository에 복사된 brAIns repository가 아닌, 원본 brAIns repository에서 우측 상단의 "Code"버튼을 눌러 HTTPS 주소를 복사합니다. 또는 다음 주소를 복사하셔도 됩니다. 

    https://github.com/UNIST-brAIns/unist-brains.github.io

이후 생성된 폴더 안으로 들어가 다음 코드를 입력하여 로컬 저장소와 원격 저장소를 연동해줍니다. 로컬 저장소의 이름을 원하는 대로 설정하여 (저장소 이름)위치에 입력하시면 됩니다. 

    git remote add (저장소 이름) (복사한 주소)

예를 들어 저장소 이름을 posting으로 설정해한다고 가정하면, 다음과 같은 코드를 입력하면 됩니다.

    git remote add posting https://github.com/UNIST-brAIns/unist-brains.github.io

다음 코드를 입력하면 저장소가 제대로 연동되었는지 확인할 수 있습니다.

    git remote -v

연동된 경우 다음과 같은 화면을 볼 수 있습니다.

![remote](../assets/images/Capture0322/capture4.jpg)

여기까지 진행하면 작성을 위한 초기 설정이 완료되었습니다!
   
# 3. Branch 생성하기

블로그를 포스팅과 코드 업로드는 이렇게 생성된 로컬 저장소에서 진행하게 되는데, 그 전에 branch를 생성하는 과정이 필요합니다. 다음 코드를 입력하여 branch를 생성하고 동시에 해당 branch로 전환합니다. branch 이름은 자유롭게 설정해주시면 됩니다.

    git switch -c (branch 이름)


다음 코드를 입력하여 branch가 잘 생성되었는지 확인할 수 있습니다.

    git branch


이렇게 branch 설정이 완료된 이후에 포스팅과 업로드를 로컬 저장소에서 진행하시면 됩니다.

# 4. 작성 위치와 방법

먼저 블로그 포스팅의 경우, md 파일 형태로 작성해 주시면 됩니다. md 파일의 경우 text editor를 사용하여 새 파일을 생성할 때 확장자 .md를 파일명 뒤에 붙여 생성할 수 있습니다.   

md 파일 같은 경우에는 [Markdown](https://gist.github.com/ihoneymon/652be052a0727ad59601)문법을 사용하여 작성하는데, 링크를 통해 문법을 확인하실 수 있습니다.   
블로그 포스팅 글을 작성하실 때 제목과 작성자, 태그를 표시해야 한다는 점을 제외하고는 모두 자유롭게 작성하셔도 됩니다.   

![기본 양식](../assets/images/Capture0322/capture5.jpg)

md 파일의 이름은 포스팅 글을 작성한 날짜와 영문 제목으로 설정해주시고, 제목과 태그, 작성자를 다음과 같이 맨 위에 작성해주시면 됩니다. 이후에는 자유롭게 작성하시면 됩니다!   
작성을 완료하신 경우, 작성이 완료된 md 파일을 **_post** 폴더에 넣고 commit,push 과정을 진행하시면 됩니다. (다음 단원에 설명이 있습니다!)   

코드 공유의 경우 각 스터디에서 지정한 형식으로 코드를 작성해 주시면 됩니다. 작성이 완료된 코드를, 스터디에서 공지한 지정 위치에 넣고 commit,push 과정을 진행하시면 됩니다.
   

# 5. 파일 Commit,Push

작성된 파일을 연동한 폴더의 지정 위치에 넣은 뒤에는, commit과 push를 통해 brAIns 데이터베이스에 이를 반영시켜 주는 과정이 필요합니다. **Commit,Push 과정을 진행하지 않으면, 작성한 파일이 로컬 디렉토리에만 존재하게 되고, 메인 저장소에는 반영되지 않기 떄문에 필수적으로 진행해야 합니다!** 초기 설정을 할 때와 같이 연동한 폴더에서 git command 창을 열어줍니다.   

새로 작성하거나 수정한 파일의 이름을 복사하여 다음 코드를 입력합니다. 이 과정을 통해 staging erea에 작성 파일을 등록하게 됩니다.

    git add (파일명)


변경된 파일 전부를 동시에 add하고 싶을 떄에는 다음 코드를 사용할 수 있습니다.

    git add .


다음 코드를 입력하여 staging erea에 있는 작성 파일을 로컬 저장소에 commit합니다.

    git commit -m (원하는 메세지)


원하는 메세지는 자유롭게 작성하시면 되고, 주로 commit하는 파일 또는 수정 사항이 무엇인지를 간단히 입력하고는 합니다. (자세한 코멘트는 조금 더 진행한 후에 작성하게 됩니다.)

다음 코드를 입력하여 로컬 저장소의 변경 사항을 메인 저장소에 업데이트합니다.

    git push origin (branch 이름)

푸시 과정에서 github와 git bash 간의 연동 허용 창이 뜨기도 하는데, 허용해줍니다. 푸시가 완료된 후 github 페이지로 이동해 fork한 brAIns repository로 들어가면 다음과 같은 초록색 "Compare & pull request" 버튼이 활성화됩니다.

![CP request](../assets/images/Capture0322/capture6.jpg)

활성화된 버튼을 누르고, comment에 어떤 내용을 추가하거나 변경하였는지 적은 뒤, "Create pull repuest" 버튼을 누르면 완료됩니다.

---

여기까지 진행하시면 블로그 포스팅과 코드 업로드 과정이 모두 완료되었습니다! (축하드립니다!) 업로드 과정에 문제가 있거나 도움이 필요한 경우 언제든지 연락 주셔도 좋을 것 같습니다.   

---
# 6. F&Q
아래는 제가 블로그 작성을 하면서 들었던 궁금증이나, 도움이 되었던 것들을 간단하게 적어 보았습니다.

* git add,commit,push 등이 잘 이루어졌는지 확인하고 싶습니다! 
    * 다음 코드를 git command 창에서 입력하면 현재 상태와 다음으로 어떤 작업을 해야 하는지에 대한 안내 문구를 출력할 수 있습니다. <pre><code>git status</code></pre>
    현재 어떤 파일이 변경되었는지, 어떤 명령어를 다음으로 작성해야 할지에 대한 정보를 얻을 수 있어 편리합니다.

* git push가 잘 되지 않습니다!
    * 원격 저장소 내용이 변경되었지만, 로컬 저장소에는 내용이 업데이트 되지 않아 발생하는 문제일 수 있습니다.<pre><code>git pull</code></pre>
    위 코드를 입력한 뒤 다시 push를 시도해 보세요!

* 블로그 포스팅을 위해 작성한 Markdown 파일에 사진을 첨부하고 싶습니다! (or 자꾸 파일에 첨부한 사진이 잘 보이지 않습니다!)
    * 올리고자 하는 사진을 brAIns 저장소 안의 assets/images 폴더에 넣은 뒤 위치를 다음과 같이 지정해줍니다.
    <pre><code>../assets/images/(이미지 파일 이름)</code></pre>
    경로 설정 방법에 관한 더 자세한 내용은 [여기](https://webfoxrain.tistory.com/11)에서 확인하실 수 있습니다. 상대경로에 대한 부분을 확인하시면 좋을 것 같습니다.

* md 파일은 [Notion](https://www.notion.so/ko-kr/product)에서 글을 작성한 뒤에 내보내기 버튼을 통해 생성하는 것도 가능합니다! 내용을 notion으로 작성하고 md파일로 만든 뒤, 제목과 태그를 달아주면 편리하게 사용할 수 있습니다.

* md 파일을 처음 작성해서 문법이 생소하거나, 어떻게 작성해야 할지 잘 모르겠다면 먼저 작성하신 분들이 어떤 문법을 사용했는지 확인해보는 것도 도움이 많이 됩니다. _posts 폴더 안의 다른 md파일을 열면 다른 분들이 포스팅한 글을 바로 확인하실 수 있습니다!

---
감사합니다!
