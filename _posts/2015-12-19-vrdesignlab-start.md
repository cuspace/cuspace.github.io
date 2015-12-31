---
layout: post
title:  "Unity VR 1: VR Design Lab 시작 부분"
date:   2015-12-19 02:12:00
categories: jekyll update
---


## 검색하다가

[Reddit 에 올라온 글][1] 을 보니, Google Design Lab source 가 없어서 직접 만들었다는 내용.
오픈소스이니 기여해 달라는 부탁. [관련 작업 진행 공유를 위한 트렐로][2] 를 통해 작업 상황을 볼 수 있다.

## 실행해보려면

* [Github VRDesignLab 소스][3] 를 받는다.
* Unity 를 실행시키고, File > Open Project … 로 해당 폴더를 선택한다.
* [Project Window][4] > Scenes > VRDL_Start 를 선택해서 scene 을 연다.
* [Toolbar Play 버튼][4] 을 눌러 [Game View Window] 에 VR 화면이 나오는 것을 확인.
![vrdl_play.jpg]({{site.url}}/assets/vrdl_play.jpg)

## 시작 부분 분석

### 어디가 시작점인가?

* [Hierarchy Window][4] 에 보이는 `App Boot Strap` 라는 이름을 가진 ~~[Game Object][5]~~ ( 아 아니구나 다시 확인해 보니 [Prefab][8]) 을 클릭해보면,  [Inspector Window][4] 에, `App Boot Strap (Script)` 라는 이름을 가진 [Script][6] [Component][7] 를 볼 수 있다. 이것이 시작점.

### 그 시작점에서는 무슨 일을 하는가?

* 해당 컴포넌트내에서 오른쪽 상단을 보면 기어 모양의 아이콘이 있다. 그 아이콘을 클릭해서 제일 아래에 `Edit Script` 항목을 눌러보자.
* Unity 와 연결된 Editor 가 실행되면서 `AppBootStrap.cs` 라는 유니티용 C# 스크립트 파일이 열린다.
* `AppBootStrap` class 안을 보면, public 으로 선언한 여러 GameObject 들을 볼 수 있다. 이렇게 public 으로 선언한 것들은 [Inspector Window][4] 에서 보면 실제 GameObject 들을 [Project Window][4] 에서 마우스로 끌어다 놓는 방식으로 변수와 실제 GameObject 를 연결할 수 있다. 참고로 `AppBootStrap`은  그렇게 초기화 해 놓은 GameObject 를 Prefab 으로 만들어 놓은 것이다.
* 그 밑에는 `Awake` 가 보이는데, Play 버튼을 누르면 `void Awake()` 가 호출될 것이다. (참고: [이벤트 함수들의 실행순서][9])
* 이 함수에서는 `AppCentral` 이 있으면 재사용하고, 없으면 만들고 초기화한다.
* 새로운 GameObject 를 만들고,
	* `transform` 초기화
	* `AppCentral` 추가 및 초기화 (미리 연결해 둔 GameObject Prefab 들로)
	* `app.Initialize()` 를 호출해서 추가 초기화 작업 진행.
* Prefab 이름을 살펴보면,
	* 카드보드용으로 빌드할 것인지 말 것인지
	* 카드보드 카메라
	* 오큘러스 카메라
	* reticle ?
	* 아래쪽을 바라봤을 때 나오는 메뉴
	* 아래쪽을 바라봤을 때 나오는 공지
	* 카메라 페이드 화면
	* 메인 화면
	* 메인 씬인지 아닌지
	* 산
	* 숲


[1]: https://www.reddit.com/r/oculus/comments/3sqckv/vr_design_lab_an_open_sourced_unity_project/
[2]: https://trello.com/b/V6xU9a4Y/vr-design-lab
[3]: https://github.com/VRUX-CO/VRDesignLab
[4]: http://docs.unity3d.com/Manual/LearningtheInterface.html
[5]: http://docs.unity3d.com/Manual/class-GameObject.html
[6]: http://docs.unity3d.com/Manual/CreatingAndUsingScripts.html
[7]: http://docs.unity3d.com/Manual/Components.html
[8]: http://docs.unity3d.com/Manual/Prefabs.html
[9]: http://docs.unity3d.com/Manual/ExecutionOrder.html
