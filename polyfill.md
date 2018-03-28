<!-- TITLE: Polyfill -->
<!-- SUBTITLE: 브라우저에서 지원하지 않는 기능을 구현한 코드이다 -->

# Polyfill
## 정의
브라우저에서 지원하지 않는 기능을 구현한 코드이다.


## 예시

Javascript (ES6 이상) 에는 String 타입의 내장 메서드로 includes() 가 존재한다. 그러나 Javascript 를 컴파일하는 브라우저에서 지원하지 않으면 사용하지 못한다. 2018-03-02 기준으로 대부분의 브라우저에서 includes()를 지원하지만, (그 놈의) IE 에서는 지원하지 않는다.

따라서 다음 코드를 내 코드에 끼워넣는다.

```
if (!String.prototype.includes) {
  String.prototype.includes = function(search, start) {
    'use strict';
    if (typeof start !== 'number') {
      start = 0;
    }
    
    if (start + search.length > this.length) {
      return false;
    } else {
      return this.indexOf(search, start) !== -1;
    }
  };
}
```

IE 에서는 `String.prototype.includes` 가 존재하지 않기 때문에 기능이 똑같은 함수를 대신 넣어주고 사용한다.  이런 방식으로 브라우저에 없는 기능을 직접 끼워넣는 코드를 Polyfill 이라고 한다.


## 한탄

크롬으로만 개발하다가 나중에 IE 로 들어가면 에러로 떡칠이 되어 있을 가능성이 높다. 그때마다 쓰레기통을 뒤적이는 고양이마냥 polyfill 을 주우러 MDN, Stackoverflow 등을 돌아다니는 본인의 모습을 보게 될 것이다.

좀 더 나은 해결책은 대부분의 스펙을 모듈로 구현해놓은 core-js 를 프로젝트에 끼워서 필요한 스펙을 사용하거나, babel을 빌드 과정에 끼워서 필요한 모든 스펙을 자동으로 포함하도록 하는 것이다.




