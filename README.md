## babel 전체 설정 파일과 지역 설정 파일

#### 전체(project-wide) 
- 모든 자바스크립트 파일에 적용되는 전체 설정파일
- 바벨 버전 7에 추가된 babel.config.js 파일

#### 지역(file-relative)
- .babelrc, babelrc.js, package.json

## 바벨과 폴리필
- 자바스크리트의 최신 기능을 모두 사용하면서 오래된 브라우저를 지원하려면 바벨로 코드 문법을 변환하는 동시에 폴리필도 사용해야한다.
- 폴리필은 런타임에 기능을 주입하는 것 
- 런타임에 기능이 존재하는지 검사해서 기능이 없는 경우에 주입
- 바벨을 사용하더라도 폴리필에 대한 설정은 별도로 해야함.

### core-js 모듈의 모든 폴리필 사용하기
core-js 는 바벨에서 폴리필을 위해 공식적으로 지원하는 패키지
가장 간단한 사용법은 core-js 모듈을 자바스크립트 코드로 불러오는 것

core-js 모듈의 사용 예
```javascript
import 'core-js';

const p = Promise.resolve(10);
const obj = {
    a: 10,
    b: 20,
    c: 30
};
const arr = Object.values(obj);
const exist = arr.includes(20)
```

웹팩을 사용하는 경우에 다음과 같이 Entry 속성에 core-js 모듈을 넣는다.
core-js 모듈은 사용법이 간단하지만, 필요하지 않은 폴리필까지 포함되므로 번들 파일의 크기가 커진다.

웹팩에서 core-js 모듈을 사용한 예
```javascript
module.exports = {
    entry : ["core-js", "./sr/index.js"],
}
```

### core-js 모듈에서 필요한 폴리필만 가져오기
core-js 로 부터 직접 필요한 폴리필만 가져오면 번들 파일의 크기를 줄일 수 있다.

core-js 에서 필요한 폴리필을 직접 넣는 코드 
```javascript
    import 'core-js/features/promise';
    import 'core-js/features/object/values';
    import 'core-js/features/array/includes';

    const p = Promise.resove(10);
    const obj = {
        a:10,
        b:20,
        c:30,
    };
    const arr = Object.values(obj);
    const exist = arr.includes(20)

```