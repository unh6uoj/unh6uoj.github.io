---
title: "GitHub 인증 오류? Support for password authentication was removed"
categories:
    - error
tags:
    - git
    - gitHub
toc: true
toc_sticky: true
---

## GitHub 토큰 발급 및 인증하기

![Git_Error](/images/git/git_error.png){: width="50%" height="50%"}
> remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
> remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.

잘 진행하던 프로젝트를 pull하려고 하다가 갑자기 auth관련 에러가 났다...  
분명 비밀번호를 맞게 입력 했는데 잘 찾아보니 GitHub에서 이제 비밀번호 인증을 없앤다고 한다.  

그래서 이걸 어떻게 하나 보니 토큰 인증을 하라고 하는데, GitHub에서 토큰을 발급 받고 어떻게 사용하는지 알아보자 👊

### GitHub에서 토큰 발급받기 🔑

먼저, GitHub의 토큰 페이지에 접속 해야한다.
<https://github.com/settings/tokens>

![Git_Error](/images/git/git_generate_tocken.png){: width="50%" height="50%"}

접속해서 로그인을 하면 Generate new tocken이라는 버튼이 있을텐데 눌러주자.  

![Git_Tocken](/images/git/git_new_tocken.png){:width="50% height="50%}

보면 Note, Expiration, Select scopes 등 여러 옵션들이 보이는데,  Note에는 인증 토큰에 관한 메모?를 알아서 적고  
Expiration엔 토큰 유통기한 설정,  
Select scopes에는 토큰에 대한 여러가지 접근 권한들을 설정 할 수 있다.  

여기까지 진행 하고 하단에 Generate tocken을 눌러주면 토큰 생성은 완료된다! 👍  

![Git_Tocken_Button](/images/git/git_generate_tocken_btn.png){:width="50% height="50%}


![Git_Tocken_Complete](/images/git/git_complete_tocken.png){:width="50% height="50%}

그러면 이런 창으로 넘어가는데, 아까 작성한 토큰메모_토큰번호 이렇게 나와있을텐데, 빨간 화살표를 누르면 복사를 할 수 있다.  

하단에는 내가 이전에 만들어둔 토큰에 대한 정보니까 화면이 달라도 무시하자!  


### GitHub 토큰 사용하기  
이렇게 발급한 토큰은 그냥 이전에 clone등에 사용하면 username, pw 인증에서 pw자리에 토큰 번호를 넣으면 된다!👏  
그리고 macOS를 사용하는 유저들은 키체인에 GitHub인증 정보를 담아두어서 사용하는 일이 많았을텐데, 키체인에 접근해서 GitHub로그인 정보를 제거하면 된다.  

아, 그리고 아까 발급 받을 때 확인한 토큰 번호는 한 번 넘어가면 절대 다시 볼 수 없기 때문에 따로 저장을 해놓는것이 유용하다.  
혹시 토큰번호를 잃어버리면 재발급을 받을 수 있으니까 크게 걱정할 것은 없지만 인증했던 모든 git파일에 재인증을 해야하는 번거로움이 있다.  

![Git_Tocken_Complete](/images/git/git_regenerate_tocken.png){:width="50% height="50%}