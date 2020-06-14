=소개
==강의 소개==
프론트엔드 개발환경의 이해와 실습
https://www.inflearn.com/course/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD/dashboard

강좌 블로그
https://jeonghwan-kim.github.io/

프론트엔드 개발에 Node.js가 필요한 이유
https://jeonghwan-kim.github.io/series/2019/12/09/frontend-dev-env-npm.html

=NPM=
==프로젝트 생성==

==외부 패키지를 관리하는 방법==
https://jeonghwan-kim.github.io/series/2019/12/09/frontend-dev-env-npm.html

CDN : 콘텐츠 전송 네트워크, CDN 서버가 장애가 발생하면 
그래서 직접 다운로드하기도 함

$ npm install react
package.json에 추가됨
```
"dependencies": {
    "react": "^16.13.1"
  }
```

유의적 버전
https://semver.org/lang/ko/
v16.12.0
주버전이 16, 부버전이 12, 수버전이 0
주 버전(Major Version): 기존 버전과 호환되지 않게 변경한 경우
부 버전(Minor version): 기존 버전과 호환되면서 기능이 추가된 경우
수 버전(Patch version): 기존 버전과 호환되면서 버그를 수정한 경우

버전의 범위
틸트(~)는 마이너 버전이 명시되어 있으면 패치버전만 변경한다. 예를 들어 ~1.2.3 표기는 1.2.3 부터 1.3.0 미만 까지를 포함한다. 마이너 버전이 없으면 마이너 버전을 갱신한다. ~0 표기는 0.0.0부터 1.0.0 미만 까지를 포함한다.

캐럿(^)은 정식버전에서 마이너와 패치 버전을 변경한다. 예를 들어 ^1.2.3 표기는 1.2.3부터 2.0.0 미만 까지를 포함한다. 정식버전 미만인 0.x 버전은 패치만 갱신한다. ^0 표기는 0.0.0부터 0.1.0 미만 까지를 포함한다.

$ npm view react versions
package.json 의 버전을 ~0으로 수정 후
$ npm install
$ cat node_modules/react/package.json 
버전이 변경되어 있음
다시 ^0.0으로 수정 후
$ npm install
$ cat node_modules/react/package.json 
다시 버전이 변경되어 있음

=웹팩(Webpack) - 기본편=
https://jeonghwan-kim.github.io/series/2019/12/10/frontend-dev-env-webpack-basic.html
==웹팩이 필요한 이유와 기본 동작==
배경
위 코드는 모두 하나의 HTML 파일 안에서 로딩해야만 실행된다. math.js가 로딩되면 app.js는 이름 공간에서 ‘sum’을 찾은 뒤 이 함수를 실행한다. 문제는 ‘sum’이 전역 공간에 노출된다는 것. 다른 파일에서도 ‘sum’이란 이름을 사용한다면 충돌한다.
IIFE 방식의 모듈

CommonJS 방식 모듈
CommonJS는 자바스크립트를 사용하는 모든 환경에서 모듈을 하는 것이 목표다. exports 키워드로 모듈을 만들고 require() 함수로 불러 들이는 방식이다. 대표적으로 서버 사이드 플래폼인 Node.js에서 이를 사용한다.

AMD
AMD(Asynchronous Module Definition)는 비동기로 로딩되는 환경에서 모듈을 사용하는 것이 목표다. 주로 브라우져 환경이다.

UMD
UMD(Universal Module Definition)는 AMD기반으로 CommonJS 방식까지 지원하는 통합 형태다.

표준모듈시스템
이렇게 각 커뮤니티에서 각자의 스펙을 제안하다가 ES2015에서 표준 모듈 시스템을 내 놓았다. 지금은 바벨과 웹팩을 이용해 모듈 시스템을 사용하는 것이 일반적이다.

```
export function sum(a, b) { return a + b; }
```
```
import * as math from './math.js';
math.sum(1, 2); // 3
```

lite-server?
$ npx lite-server

==엔트리/아웃풋 실습==
https://webpack.js.org/
Webpack은 번들러

webpack, webpack-cli 설치
$ npm install -D webpack webpack-cli

웹팩으로 번들링
node_modules/.bin/webpack --mode development --entry ./src/app.js --output dist/
main.js

dist/main.js 생성 확인

index.html의 script부분을 변경
```
<script src="dist/main.js"></script>
```

웹팩설정파일 생성
webpack.config.js
```
const path = require('path');

module.exports = {
    mode: 'development',
    entry: {
        main: './src/app.js'
    },
    output: {
        path: path.resolve('./dist'),
        filename: '[name].js'
    }
}
```

package.json의 build에 등록
```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
},
```

==엔트리와 아웃풋(실습)
https://github.com/jeonghwan-kim/lecture-frontend-dev-env/packages

강의 중 실습은 아래 브랜치 중 하나로 이동하여 진행합니다. 브랜치를 이용하면 각 실습에서 풀어야하는 문제가 TODO 주석으로 기록되어 있습니다.

1-webpack/1-entry: 웹팩 엔트리/아웃풋 실습
1-webpack/2-loader: 웹팩 로더 실습
1-webpack/3-plugin: 웹팩 플러그인 실습
2-babel/1-babel: 바벨 실습
2-babel/2-sass: 사스 실습
3-lint/1-eslint: 린트 실습
3-lint/2-prettier: 프리티어 실습
4-webpack/1-dev-server: 웹팩 개발 서버 실습
4-webpack/2-hot: 웹팩 핫로딩 실습
4-webpack/3-optimazation: 웹팩 최적화 실습
5-sample/1-react: 리액트 샘플 실습
master: 최종 결과물
