---
layout: post
title:  "[Github blog] Jekyll을 이용한 github blog 구축하기"
date:   2019-11-09 17:18:00
categories: Blog
tags: GitHub-Blog Jekyll
---

개인적으로만 공부하다가 공부한 내용을 정리할 필요성과 이력관리의 중요성을 깨달으면서 깃허브 블로그를 시작하게 되었다. 웹서버의 역할은 깃허브에서 모두 제공하며, 레이아웃 또한 사람들이 미리 만들어 놓은 것을 사용하였다. 세부적인 내용이나 옵션은 생략하고, 중요한 내용을 우선적으로 다루려고 한다.

## 1. 레포지토리 만들기
레포지토리의 이름은 기본적으로 다음 형식을 따른다.
- `[깃허브 계정명].github.io`

![](https://github.com/ByoungJoonIm/ByoungJoonIm.github.io/blob/master/captures/2019-11-09-Github-Blog-001.jpg?raw=true)

## 2. Theme 고르고 업로드 하기
Jekyll은 많은 사람들이 미리 레이아웃을 만들어 놓았고, 우리는 고르기만 하면 된다. [여기](https://github.com/topics/jekyll-theme)에서 theme을 고르자. 예를 들어서 mmistakes/minimal-mistakes을 고른 경우 다음 링크를 클릭하면 해당 사이트를 직접 볼 수 있다.
![](https://github.com/ByoungJoonIm/ByoungJoonIm.github.io/blob/master/captures/2019-11-09-Github-Blog-002.jpg?raw=true)

Theme을 골랐다면, 해당 프로젝트를 Zip으로 다운받는다.

![](https://github.com/ByoungJoonIm/ByoungJoonIm.github.io/blob/master/captures/2019-11-09-Github-Blog-003.jpg?raw=true)

해당 프로젝트의 압축을 풀어 아까 만든 레포지토리에 업로드한다.

![](https://github.com/ByoungJoonIm/ByoungJoonIm.github.io/blob/master/captures/2019-11-09-Github-Blog-004.jpg?raw=true)

## 3. _config.yml 파일 수정하기
jekyll이 편한 이유 중 하나는, 우리가 코드를 크게 수정하지 않아도 _config.yml 파일만 수정하면 사이트에 바로 적용할 수 있다는 점이다. _config.yml에는 다음과 같은 내용이 들어가야 한다.
```
url                      : "https://[gitID].github.io"
baseurl                  : ""
```
그 외에 값으로 다양한 사이트(페이스북, 깃허브, 링크드인 등)를 손쉽게 연결할 수 있다.

## 4. 확인하기
위 과정이 완료되었다면 다음 주소로 접속하여 확인한다.
- `https://[gitID].github.io/`

## 그 외 팁
### 프로젝트를 수정할 때
프로젝트를 수정할 때 주의할 점은, 만약 파일을 잘못 삭제하거나 수정해서 빌드가 실패하게 되면 github는 마지막으로 빌드한 사이트를 제공한다. 이러한 빌드 실패는 2가지 방법으로 확인할 수 있다.

![](https://github.com/ByoungJoonIm/ByoungJoonIm.github.io/blob/master/captures/2019-11-09-Github-Blog-005.jpg?raw=true)

commits에서 확인하는 경우, 다음과 같이 에러 메시지도 함께 확인이 가능하다.

![](https://github.com/ByoungJoonIm/ByoungJoonIm.github.io/blob/master/captures/2019-11-09-Github-Blog-006.jpg?raw=true)

### 수정한 뒤 페이지가 반영이 안될 때
보통 이런 경우는 다음의 경우 발생한다.
- 배포가 아직 안된 경우 : 약간의 시간을 기다린다.(즉시 반영될정도로 github에서 제공하는 서버 성능이 빠르지는 않다.)
- 배포가 실패한 경우 : 위의 `프로젝트를 수정할 때`를 참고하여 해결한다.
- 캐시에 저장된 내용이 보이는 경우 : 크롬 기준으로 `F12`를 눌러 개발자 도구를 연 뒤, 새로고침을 마우스 우클릭하고 `캐쉬 비우기 및 강력 새로고침`을 누른다.

![](https://github.com/ByoungJoonIm/ByoungJoonIm.github.io/blob/master/captures/2019-11-09-Github-Blog-007.jpg?raw=true)

## Reference 및 기능 추가를 위해 참조하면 좋은 사이트
- [쉽고 빠르게 수준 급의 GitHub 블로그 만들기 - jekyll remote theme으로](https://dreamgonfly.github.io/2018/01/27/jekyll-remote-theme.html)


