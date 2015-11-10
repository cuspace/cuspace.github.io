---
layout: post
title:  "VR 1: VR 제작환경(three.js 사용)"
date:   2015-10-24 15:18:00
categories: jekyll update
---
웹브라우저에서 동작하는 VR 을 만들어 봅시다.  
이 글에서는 다음과 같은 것들을 사용할거예요.

* [three.js][2] 및 함께 제공되는 VR 관련 파일들
* [Brackets][1]
* 최신 PC 웹브라우저
* 스마트폰 최신 모바일 웹브라우저
* [python][5]
* [구글카드보드][4]


## Brackets 설치, 작업폴더 및 파일 생성

* [Brackets][1]를 다운로드, 설치, 실행 합니다.
* `파일 > 폴더열기` 를 클릭하고, 	 
![folder_open]({{site.url}}/assets/folder_open.jpg)
* `New Folder`를 눌러 작업할 폴더 이름을 입력하고,  
![new_folder]({{site.url}}/assets/new_folder.jpg)
* `Open`을 눌러 그 폴더를 엽니다.  
![open]({{site.url}}/assets/open.jpg)
* 마우스 오른쪽 버튼을 눌러 `파일 만들기`를 클릭한 후,  
![new_file]({{site.url}}/assets/new_file.jpg)
* `index.html`이라고 입력해서 파일을 만듭니다.  
![index_html]({{site.url}}/assets/index_html.jpg)

## index.html 기본 골격

* `index.html` 에 다음과 같이 입력합니다.

```html
<!DOCTYPE html>
<html>
	<head>
	</head>
	<body>
	</body>
</html>
```

## Brackets 의 실시간 미리 보기 기능 확인

* `index.html` 의 `<body></body>` 안에 다음과 같이 입력하고,

```html
<!DOCTYPE html>
<html>
	<head>
	</head>
	<body>
        <h1>TEST</h1>
	</body>
</html>
```

* `실시간 미리보기` 를 클릭하면,  
![live_preview]({{site.url}}/assets/live_preview.jpg)
* 웹브라우저가 실행되면서 미리 볼 수 있습니다.  
![live_preview_web]({{site.url}}/assets/live_preview_web.jpg)
* 이 상태에서 웹브라우저를 닫지 않고, 다시 Brackets 로 돌아가 `TEST`를 `TEST EDIT`으로 바꾸면,

```html
<!DOCTYPE html>
<html>
	<head>
	</head>
	<body>
        <h1>TEST EDIT</h1>
	</body>
</html>
```

* 수정과 동시에 그 내용이 웹브라우저에 반영되는 것을 볼 수 있습니다.  
![live_preview_web_edit]({{site.url}}/assets/live_preview_web_edit.jpg)
* 참고로 실시간 미리보기는 브라우저를 닫거나, 번개 모양의 버튼을 다시 클릭하면 종료됩니다.

## 스마트폰 브라우저에서도 보려면

* 위 상태에서, 터미널(윈도우는 cmd 창)을 열어서 압축을 푼 해당 경로로 가기  
	* 예) `cd ~/the_blah_blah_folder`
* 터미널 위 경로에서 파이썬으로 http server 실행시키기
  * python 2.x 인 경우: `python -m SimpleHTTPServer 8000` : https://docs.python.org/2/library/simplehttpserver.html
  * python 3.x 인 경우: `python -m http.server 8000` : https://docs.python.org/3/library/http.server.html
* 노트북(데스크탑)의 IP 주소 확인
  * 윈도우의 경우: cmd 창 하나 더 띄워서 `ipconfig [엔터]` : 나오는 목록 중에서 `IPv4 주소`
  * mac osx 의 경우: terminal 창 하나 더 띄우거나 tab 을 띄워 `ifconfig [엔터]` : 나오는 목록 중에서 `inet `
* 폰이 노트북과 같은 AP 에 접속되어 있는 지 확인.
* 폰 웹브라우저 실행:
  * 주소창에 입력(x는 위에서 확인한 노트북(데스크탑)의 IP 주소) : `xxx.xxx.xxx.xxx:8000/index.html`
![from_mobile_chrome]({{site.url}}/assets/from_mobile_chrome.jpg)
* 참고로 이렇게 실행시킨 http server 는 터미널 창에서 `control키(Ctrl키)+c` 를 두 번 누르면 종료됩니다.

## VR에 필요한 js 파일 다운로드 및 포함시키기

* `Brackets`에서 마우스 오른쪽 버튼을 눌러 `폴더 만들기`를 클릭해서 `js` 폴더를 만듭니다.
* [three.js github][3] 사이트의 다음 경로에서 각각의 파일을 방금
    만든 `js`폴더에 저장합니다. 다운로드 방법은 각각의 파일을 클릭한 뒤에
    `RAW`버튼을 누른 뒤에, 소스코드만 보이는 상태에서 마우스 오른쪽 버튼을 눌러
    다른 이름으로 저장합니다. (`RAW`버튼을 누르지 않고 저장하면 html 내용을
    갖고 있는 github 사이트용 파일이 저장되므로 주의하세요)
  * https://github.com/mrdoob/three.js/tree/master/build 에서, `three.js`
  * https://github.com/mrdoob/three.js/tree/master/examples/js/effects 에서 `StereoEffect.js`
  * https://github.com/mrdoob/three.js/tree/master/examples/js/controls 에서 `OrbitControls.js`
* `Brackets` 왼쪽 패널 js 폴더에 저장한 파일들이 보이는지 확인  
![dn_result_check]({{site.url}}/assets/dn_result_check.jpg)
* `index.html` 파일을 다음과 같이 수정합니다.

```html
<!DOCTYPE html>
<html>
	<head>
	</head>
	<body>
		<script src="./js/three.js"></script>
		<script src="./js/StereoEffect.js"></script>
		<script src="./js/OrbitControls.js"></script>
	</body>
</html>
```

## 앞으로 작성할 js 파일 만들기

* `Brackets`의 js 폴더에서 오른쪽마우스 클릭해서 `파일 만들기`를 눌러, `vrpractice.js` 파일을 만듭니다.
* 다시 `index.html` 을 선택해서 아래와 같이 방금 만든 파일을 포함시켜줍니다.

```html
<!DOCTYPE html>
<html>
	<head>
	</head>
	<body>
		<script src="./js/three.js"></script>
		<script src="./js/StereoEffect.js"></script>
		<script src="./js/OrbitControls.js"></script>
        <script src="./js/vrpractice.js"></script>
	</body>
</html>
```

## 다음 글에선

Three.js helper 를 이용해서 3D 공간을 눈으로 볼 수 있도록 해보고,  
Cube 나 Sphere 등을 3D 공간에 놓은 후,  
스마트폰의 웹브라우저에서 어떻게 보이는 지 확인해 보도록 하겠습니다.

### 참고

* Brackets : http://brackets.io/
* Three.js : http://threejs.org
* Three.js github : https://github.com/mrdoob/three.js/
* Google Cardboard : https://www.google.com/get/cardboard/
* Python Download : https://www.python.org/downloads/

[1]: http://brackets.io/
[2]: http://threejs.org
[3]: https://github.com/mrdoob/three.js/
[4]: https://www.google.com/get/cardboard/
[5]: https://www.python.org/downloads/
