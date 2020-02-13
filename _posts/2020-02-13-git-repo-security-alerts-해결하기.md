---
layout: post
title: git repo security alerts 해결하기
subtitle : git repo security alerts 해결하기 
tags: [django, git]
author: jylee.
comments : False
---
## git security alerts 발생
![security_alerts3](https://raw.githubusercontent.com/leejaeyeong/leejaeyeong.github.io/master/assets/img/security_alerts3.png) 
예전에 작업했던 프로젝트 저장소에서 보안 알림 표시되어 있었다.  
크게 신경을 안 쓰고 있다가 다른 django 프로젝트에도 같은 알림 표시된 것을 보고, 확인한 결과 django 버전이 문제였다.   
git은 새로운 취약성이 추가되면 종속성의 영향을 받은 버전을 사용하는 repo에 pull request을 보내고 알림을 표시한다.  
<br>

## security alerts 해결하기  
![security_alerts1](https://raw.githubusercontent.com/leejaeyeong/leejaeyeong.github.io/master/assets/img/security_alerts1.png)  
해당 저장소를 sourcetree로 확인해보면 pull request를 확인할 수 있다.  
commit message를 보면 django version 2.2.3 ~ 2.2.10, pillow version 6.1.0 ~ 6.2.0에서 보안 알림이 발생한다는 것을 알 수 있다.  
해결 방법은 단순히 보안 이슈가 해결된 **버전으로 업그레이드** 하는 것이다.
위 경우 django는 최소 2.2.10 버전 , pillow는 최소 6.2.0 버전으로 업그레이드 하는 것으로 문제를 해결할 수 있다. 

<br>

![security_alerts2](https://raw.githubusercontent.com/leejaeyeong/leejaeyeong.github.io/master/assets/img/security_alerts2.png)  
해당 pull request와 master branch를 병합한다.

<br>

```
pip install --upgrade django==2.2.10
pip install --upgrade pillow==6.2.0
```
django와 pillow 버전 업그레이드를 진행한다.  

<br>  

```
pip freeze > requirements.txt
```
django 패키지 변경사항이 발생하면 requirements를 잊지말자!

버전 업그레이드를 마치고 저장소에 push하면 보안 알림이 사라진 것을 확인할 수 있다. 