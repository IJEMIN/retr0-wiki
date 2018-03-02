<!-- TITLE: Polyfill -->
<!-- SUBTITLE: A quick summary of Polyfill -->

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







