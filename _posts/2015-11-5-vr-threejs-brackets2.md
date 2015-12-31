---
layout: post
title:  "VR 2: three.js 기본구조"
date:   2015-11-5 11:00:00
categories: jekyll update
---

## 기본 틀이 되는 구조

`vrpractice.js` 의 기본 구조입니다.

```javascript
init();
animate();
function init() {
}
function animate() {
}
```

`init()`은 처음에 한번만 호출되도록 하고,
`animate()`는 animation 을 웹브라우저에 표현할 수 있도록 반복해서 호출되게 하고
싶습니다.
그러기 위해 [requestAnimationFrame][1] 을 사용하도록 코드를 수정합니다.

```javascript
init();
animate();
function init() {
}
function animate() {
    requestAnimationFrame(animate);
}
```

## Container

html tag 중 하나인 `<div></div>` 를 코드로 만들고 html body 에 추가 합니다.
후에 WebGL을 그릴 html element 를 이 태그 밑에 추가할 것입니다.

```javascript
var container;
init();
animate();
function init() {
  container = document.createElement('div');
  document.body.appendChild(container);
}
function animate() {
  requestAnimationFrame(animate);
}
```

이 상태에서 Brackets 의 번개모양 아이콘을 누르면([이전 글][3] 참고), 브라우저에 빈 화면이 뜰텐데요.
[크롬 개발자도구][2] 를 열어서 (윈도우: `Ctrl+Shift+I`, 맥: `Cmd+Opt+I`), `Elements`를 누르면,
다음과 같이 div 가 추가된 것을 볼 수 있습니다.

![chrome_dev_div]({{site.url}}/assets/chrome_dev_div.jpg)

## WebGL Renderer

WebGL 로 그릴 `<canvas>` tag 를 `<div></div>` 밑에 추가 합니다.  
이를 위해 `renderer` 라고 이름붙인 변수를 사용할 것이고, `THREE.WebGLRenderer()` 를 이용해서 만들 것입니다.

```javascript
var container, renderer;
init();
animate();
function init() {
  container = document.createElement('div');
  document.body.appendChild(container);

  renderer = new THREE.WebGLRenderer();
  container.appendChild(renderer.domElement);
}
function animate() {
  requestAnimationFrame(animate);
}
```

이 상태에서 Brackets 의 번개모양 아이콘을 누르고, 크롬 개발자도구의 `Elements`를 보면 다음과 같이 `<div>` 아래에 `<canvas>` 가 만들어진 것을 볼 수 있습니다.

![chrome_dev_div_canvas]({{site.url}}/assets/chrome_dev_div_canvas.jpg)

[1]: https://msdn.microsoft.com/en-us/library/hh920765(v=vs.85).aspx
[2]: https://developer.chrome.com/devtools
[3]: http://cuspace.github.io/jekyll/update/2015/10/24/vr-threejs-brackets1.html
