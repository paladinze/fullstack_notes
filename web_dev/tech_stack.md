# Web dev tech stack

## FE (JS)
- lanaguage：JS + TS (type enhancement)
- styling: css
  - layout: flexbox, grid
  - architecture: 
    - css module, 
    - 7-1 architecture
  - libraries: umi, dva, antd
  - preprocessor: sass, less
- utility: lodash, rxjs, ramda(fp)
- bundler: webpack, rollup
- frameworks:
  - desktop UI framework: React, Vue, Angular
  - mobile UI framework：React native, flutter, Ionic
  - server side render: Next
    - React Hooks for Remote Data Fetching： https://swr.now.sh/
  - fullscreen scrolling sites: fullPage.js
- statement management：Redux，Redux saga，mobx, vuex
- stylecheck: ESLINT, TSLint
- testing：Jest, Enzyme，cypress
- design sharing：zeplin，storybook
- IDE：VS Code，Webstorm
- version control：git
- design pattern：Micro FE	
- ecosystem
  - React
    - router: react-router
    - mobile framework: react-native
  - http request: axios 
  - state management: redux
    - reselect, redux-thunk
    - redux-actions, react-native-router-flux
    - react-native-maps, redux-offline
  - form: formik, redux-form
  - animation: animeJs
  - chart:
    - chartjs
    - d3, echarts(baidu)
  - presentation: revealJs
  - embed video: videoJs
  - 3d webgl rendering: webGL
  - 2d webgl rendering: pixiJs
  - template engine: handlebar
  - audio library: HowlerJs
  - gis: SuperMap, ArcGIS, GeoServer
  - socketis: realtime communication
  - simple static server for testing: server

## BE (JS) 
- runtime: NodeJs
- framework
  - REST: Express, Nest
  - Graphql: Apollo, TypeGraphql
  - query builder: knex
  - orm: TypeORM, sequelize, objection.js, mongoose
  - middlewares:
    - set http response headers to enhance security: helmet
- database
  - sql: psql, mysql
  - nosql: mongo
  - cache: Redis
  - analytic: elasticsearch
- pipeline
  - container: Docker + Kubernates
  - cicd: gocd, jenkins
  - fastlane: ios & android build
  - terraform: pipeline as code

## BE (Java)
- 语言：Java, kotlin, Scala, Gradle
- 框架：Spring Boot, Spring Cloud
- db migration automation: flyway
- 测试：MockK for kotlina
- Prometheus, EFK
- Kafka
- reactiveX: API for asynchronous programming
- Packer: build machine images
- secrets as a service: git-secrets and Talisman
- Monitoring
  - 分析与检测：Grafana

## style guides
- Airbnb JavaScript Style Guide

## software as a service
- Realtime collaboration using markdown: codimd
- take screenshot of code: carbon
  - https://carbon.now.sh/

## cloud provider
- deployment of static pages
  - sh
  - next.js now
  - netlify
- vps: aws, aliyun, tencent cvm
- backend as service: leancloud
- image service: qiniuyun

## public apis
- JSONPlaceholder: fake online rest api for testing 
- TV api: https://www.tvmaze.com/api
- weather: darksky.net

## learning resources
- [33 JS Concepts](https://github.com/leonardomso/33-js-concepts)
- [algorithms in JS](https://github.com/trekhleb/javascript-algorithms)
- You Don’t Know JS Yet	- Kyle Simpson
- clean code practices
  - [clean code JS](https://github.com/ryanmcdermott/clean-code-javascript)
- css playground
  - css flexbox: http://flexboxfroggy.com/
  - css grid: http://cssgridgarden.com/
- Real World examples: realworld
- [front-end deployment checklist](https://github.com/thedaviddias/Front-End-Checklist)
