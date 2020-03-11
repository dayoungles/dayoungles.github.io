---
layout: post
title: IntelliJ Live template
categories: [IntelliJ,Productivity]
---

내가 사랑하는 Intellij는 사소한 반복을 줄여서 productivity의 향상을 지원하고, 이것은 곧 나의 Performance에 영향을 미친다.

카카오를 퇴사하면서 사용하던 인텔리제이 설정을 export하지 않았다. 그 때 당시에는 내가 해놓은 설정이 그렇게 소중하다는 생각을 해본 적이 없었다. 하지만 몇 년 간의 습관이 하나하나 쌓여 Intellij 에 설정되어 있었다. 모두 다 내 생산성에 큰 영향을 미치는 자산인데 그 때는 하나씩 하나씩 설정했던 것들이 그렇게 많다고 체감하지 못했던 것이다.(그리고 설정을 밀고...회사 컴을 새로 받고...갠컴도 새로 사고...지금은 습관에 맞춰 설정을 찾아가는 상태)

그 중에서도 없으면 불편한 줄 모르고 쓰지만 있으면 또 중독되는 것이 Live template이다. 입사 초기에 시니어 개발자 분이 알려주셔서 늘 유용하게 써먹고 있다(THX to Dex). 그런데 오랜만에 새로운 설정을 하러 들어갔더니 원하는대로 동작하지 않아서 확인하던 차에, 이 라이브 템플릿을 입력하는 창 아래에 있는 **No applicable contexts**를 클릭해서 사용하려는 언어로 셋업해줘야 동작한다는 것을 다시 기억해냈다. 이건 영어로 된 문서에도 나와 있지만 누가 문서를 그렇게 열심히 읽겠는가. 그래서 놓쳤다. 

겸사 겸사 읽으러 들어간 문서에 이미 정의되어 있는 live template에서 사용 가능한 함수 등을 새롭게 발견해서 덧붙인다. 

예를 들어 아래와 같은 라이브 템플릿을 만든다고 가정하면 

```java
for (int i = 0; i < $END$; i+) {
	// created on $DATE$ by $USER$
}
```
edit variable 세팅에서 이미 정의된(predefined) date() 함수를 $DATE$에 할당해서 오늘 날짜가 자동으로 입력하고, $USER$ 에는 user() 함수를 할당해서 코드 작성자의 이름이 바로 입력되도록 할 수 있다. 이름은 그냥 내 이름 하드코딩하면 되는데...? 라고 생각했는데 이 live template을 share하는 기능도 있는 것으로 보아 다른 사람들과 공유할 때 헷갈리지 말라고 있는 기능인 듯. 

앞으로 사용할 예약어(abbreviation)를 정의하면 위의 템플릿은 아래와 같이 변경되고 변수를 확인하는 차원에서 엔터 키를 쳐주면 $END$ 변수가 정의되어 있는 위치에서 커서가 깜박거리고 기다리고 있다. 내가 채워줘야 하는 부분에 END 변수를 넣어주면 좀 더 편리하다.

평소에 자주 사용하던 sout도 내장된 라이브 템플릿의 하나였고 fori, ifn(if null) 등이 사전에 정의되어 있는 것을 확인했으니 생산성을 위해서 검토해 볼 만하다. 

나는 이미지 따위는 캡쳐해서 올리지 않는다...인터넷에 한글로 검색하면 gif 로 올라온거 많다....

[References]
[live tamplate predefined functions ](https://www.jetbrains.com/help/idea/template-variables.html)