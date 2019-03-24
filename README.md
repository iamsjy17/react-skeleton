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

### Eslint + prettier 설정(vscode)

#### eslint 설치

우선 vscode 의 market place 에서 eslint 를 찾아서 설치합니다.

#### .eslintrc 파일 추가

eslint 를 적용하기 위해 프로젝트 루트 경로에 `.eslintrc.json` 파일을 추가합니다.
바로 빨갛게 오류가 잔뜩 생기는 것을 볼 수 있으실 거에요. 일단은 무시하고 넘어갑시다.

#### prettier 설치

다음으로 market place 에서 prettier 를 설치합니다.
이 부분은 사실 필수는 아니에요. 그런데 `prettier`는 코드 포맷팅을 도와주는 plugin 으로 설치하시면 매우 편리합니다!

#### eslint 와 prettier 연동

`prettier-eslint` 를 추가합니다.

```bash
yarn add --dev prettier-eslint
```

그리고 설정을 수정하여 저장할 때마다 자동으로 prettier 를 실행하도록 하고, 또 eslint 규칙에 따라서 formatting 하도록 설정합니다.

```json
{
  "editor.formatOnSave": true,
  "javascript.format.enable": false,
  "prettier.eslintIntegration": true
}
```

#### airbnb 추가

```
yarn add eslint-config-airbnb
```

airbnb 는 가장 유명한 javascript 코딩 규칙입니다. 많은 곳에서 사용되고 있어서 이 규칙에 익숙해 지시면 _올바른_(튀지않는) 코딩 스타일을 익힐 수 있습니다.

그런데 매우 매우 까다로워서 사용하시다가 이건 좀 심하다 싶으신 것들은 꺼주시면 됩니다.

#### .eslintrc 파일 수정

그럼 .eslintrc 파일을 수정하여 airbnb 스타일을 사용하도록 합니다.
아래 rules 아래에 규칙들을 추가하여 on/off 할 수 있습니다.

```json
{
  "parser": "babel-eslint",
  "extends": "airbnb",
  "plugins": ["react", "jsx-a11y", "import"],
  "rules": {
    "react/jsx-filename-extension": 0
  },
  "env": {
    "browser": true,
    "node": true
  }
}
```

#### linting 에서 파일 제외하기

eslint 가 적용되지 않아도 되는 파일까지 포함되었다면 제외해줍니다.

```
/* eslint-disable */
```

#### NODE_PATH 인식

../../../components/header와 같이 상대경로의 depth 가 깊어지면 가독성도 좋지 않고 실수할 여지도 많아집니다. 그렇기 때문에 NODE_PATH 를 지정하여 src 경로로부터 절대경로로 사용을 합니다.

문제는 이렇게 경로를 지정했고, 잘 동작하는데 eslint 는 오류로 인식을 한다는 겁니다.

.eslintrc파일에 아래와 같이 추가하시면 해결됩니다.

```json
{
...
    "settings": {
        "import/resolver": {
            "node": {
                "moduleDirectory": ["node_modules", "src"]
            }
        }
    },
...
}
```
