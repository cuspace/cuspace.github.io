---
layout: post
title:  "VR 2: three.js helper를 이용한 공간 확인"
date:   2015-11-5 11:00:00
categories: jekyll update
---

## 기본 틀이 되는 구조 추가

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

[1]: https://msdn.microsoft.com/en-us/library/hh920765(v=vs.85).aspx
