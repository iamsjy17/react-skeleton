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
