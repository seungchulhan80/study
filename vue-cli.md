# Vue Cli

## 설치

**yarn 설치**

```
npm i -g yarn
```

**vue-cli 3.0alpha.x설처**

```
npm i -g @vue/cli
# 또는
yarn global add @vue/cli
```

**프로젝트 시작**

```
vue create [프로젝트 명]
```

**두가지 선택지 제공**

- default(babel, eslint) (babel, eslint플러그인만 포함)
- Manually select features (원하는 플러그인 선택)

## 폴더구조

```
- dist          # 산출물, build전까지 없음
- node_modules  # 의존성 파일
- public        # 공용으로 접근 가능한 파일 (favicon.ico, index.html)
- src           # 애플리케이션 소스코드
- test          # 테스트 코드
- gitignore
- package.json
```

### src

- assets: 자원 정보들이 저장, 이곳에 저장된 파일을 Vue컴포넌트에서 사용하면 build시 배포버전을 만들때 함께 포함됨
- components: vue 컴포넌트 작성하는 곳

### public

배포버전을 빌드 할때 필요한 파일. webpack을 사용해 이파일을 로드한 뒤 설정을 추가하여 빌드버전을 만듦

## script

```
"scripts": {
  "serve":"vue-cli-service serve", # 개발용 버전으로 앱실행
  "build":"vue-cli-service build", # 배포용 버전으로 앱실행
  "lint":"vue-cli-service lint"    # 코드 스타일 lint
}

vue-cli-service [command] [options]

# 옵션을 보려면
nps vue-cli-service serve --help

# 개발용 버전앱을 실행하면서 chrome으로 자동으로 오픈하려면
"serve": "vue-cli-service serve --open"으로 작성

cli

npm run serve 또는 yarn serve
```

## vue.config.js

CLI 서비스(@vue/cli-service)는 모두 캡슐화 되어 있기 때문에 내부의 웹팩에 대해 웹팩 설정 파일을 이용해 직접 설정할 수 없다. 대신 웹팩 설정을 위해 vue.config.js파을을 프로젝트 내부에 작성
[vue.config 참조](https://cli.vuejs.org/config)

## vue cli gui

터미널에서 프로젝트를 생성 관리 할 수 있지만 gui를 이용해 관리 할 수 도 있음

```
vue ui
```

## 기본구조

**public/index.html**

```
<!DOCTYPE html>
<html lang="en">

  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <title>contactapp</title>
  </head>

  <body>

    <noscript>
      <strong>We're sorry but contactapp doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>

    <div id="app"></div>
    <!-- built files will be auto injected -->

  </body>

</html>
```

**src/main.js**

```
import Vue from 'vue'
import App from './App.vue' # src/App.vue를 import

new Vue({
  render: h => h(App),      # import 'App'을 랜더린한다
}).$mount('#app')
```

**src/App.vue**

```
<template>
  <div id="app>   # 템플릿 안의 마크업 작성 할때 꼭 하나의 부모 태그 안에 작성 해야 함

    <List></List> # 소문자로 작성해도 됨, 컴포넌트명이 카멜케이스로 되어있을 경우 헝가리안 표기법? 으로 사용해도 됨
                  # 속성명은 소문자로 작성, props가 카멜케이스일때 헝가리안 표기법?으로 사용해야 됨 (html은 대소문자 구분을 하지 않음)
  </div>
</template>
<script>
  # .js , .vue 파일을 import 할 수 있음
  import List from './components/List.vue';

  export default {
    name: '' # 현재 컴포넌트의 이름 설정
    components: { # 현재 컴포넌트에서 자식으로 쓸 컴포넌트를 정의
      List
    }
  }
</script>
<style>
  # lang="sass/less..."등을 지정
  # scoped 속성을 설정하면 global로 css가 설정 되지 않고 현재 컴포넌트와 현재 컴포넌트가 갖는 자식 컴포넌트까지만 범위가 지정됨

</style>
```
