# react-skeleton

basic react project(sass, redux, eslint ...etc. )

### 프로젝트 생성

```bash
create-react-app react-skeleton
```

### eject

프로젝트 환경설정 파일들을 프로젝트 루트로 옮겨줍니다. (config폴더)

```bash
yarn eject
```

### 불필요한 파일 제거

불필요한 파일을 제거하고, 그에 맞게 index.html, app.js, index.js를 수정합니다.

deleted: src/App.css
deleted: src/App.test.js
deleted: src/index.css
deleted: src/logo.svg

modified: public/index.html
modified: src/App.js
modified: src/index.js

### sass 설정

```bash
yarn add node-sass classnames
```

1. node-sass : sass로 작성된 코드들을 css로 변환해주는 역할
2. classname : 여러개의 클래스를 한번에 주고 싶을 때 편리하게 할 수 있도록 도와주는 라이브러리

### styles 폴더 추가 (sass 파일들을 모아둘 폴더)

전역적으로 사용할 sass파일들을 모아두는 폴더입니다.
root 경로에 styles 폴더를 추가하고, 스타일 파일들을 편하게 불러올 수 있도록 path를 추가해줍니다.

```js
{
              test: sassRegex,
              exclude: sassModuleRegex,
              use: getStyleLoaders(
                {
                  importLoaders: 2,
                  sourceMap: isEnvProduction && shouldUseSourceMap,
                  options: {
                    includePaths: [paths.appSrc + "/styles"] //추가
                  }
                },
                "sass-loader"
              ),
              // Don't consider CSS imports dead code even if the
              // containing package claims to have no side effects.
              // Remove this when webpack adds a warning or an error for this.
              // See https://github.com/webpack/webpack/issues/6571
              sideEffects: true
            },
```

### Redux 추가

#### redux dependency 추가

기본적으로 리덕스를 사용하기 위해서 redux, react-redux 를 추가해줍니다.

```
yarn add redux react-dedux
```

#### Immutable 추가

`Immutable`은 리액트에서 중요한 객체 불변성을 편하게 유지할 수 있도록 도와주는 라이브러리입니다.

```
yarn add immutable
```

#### redux-actions 추가

매번 action type 을 추가 할 때마다 action 생성함수를 만드는 것이 상당히 번거롭습니다. redux-actions 는 action 생성함수를 편하게 만들 수 있도록 도와주는 라이브러리입니다.

```
yarn add redux-actions
```

### Router 추가

SPA, Single Page Application 개발을 위해서는 라우팅 기능이 필요합니다. 리액트 자체에는 이런 기능을 내장하고 있지 않기 때문에 라이브러리를 사용합니다.

#### react-router 추가

리액트 애플리케이션에서 라우팅 용도로 가장 많이 사용되는 라이브러리입니다.

```
yarn add react-router-dom
```

### NODE_PATH 설정

SPA 는 여러개의 Page 를 가지고 있기 때문에, 폴더 구조가 복잡해 질 수 있습니다. 뎁스가 깊은 폴더 내에 있는 Component 에서 다른 Component 를 참조한다면 ../../../../../ 와 같은 소스가 많이 생겨납니다.

그래서 NODE_PATH 를 지정해서 절대경로로 import 해줄 수 있도록 합니다.
.env 파일을 루트 경로에 추가하여 아래와 같이 입력합니다.

```
NODE_PATH=src
```
