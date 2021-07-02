## Vue-CLI
npm 으로 설치한 Vue CLI 로 프로젝트를 만들더라도 yarn을 요구하므로 yarn이 미리 설치되어있어야 한다.
- yarn 설치
   ` npm install -g yarn`

- vue-cli 3.0 alpha.x 설치
    `yarn global add @vue/cli`
    또는
    `npm install -g @vue/cli`
    
## package.json
기존의 Vue CLI 템플릿은 각 설정들을 가진 자바스크립트 파일을 노출한다. 
3.0버전의 목표인 사용자에게 설정을 노출함으로 인하여 발생하는 혼란을 줄이기 위해 프로젝트 설정을 packge.json 파일에 담는 것으로 제한한다.

- scripts
serve : 개발용 버전으로 앱을 실행합니다.
build : 배포용 버전으로 앱을 빌드합니다.
test : 테스트코드를 실행합니다.
lint : 코드 스타일을 lint 합니다.

## github pages
간단하게 HTML/CSS/JS 파일을 무료로 호스팅 가능하다.


## Vue-Cli 프로젝트 생성
1. vue-cli 설치 확인
    `vue -V`

2. Vue 프로젝트 생성
    `vue create vue-devops`
    프로젝트 생성 과정에서 아래와 같은 순서로 선택합니다.  
    Manual select features, Unit Testing 추가선택, 3.x, EsLint + Prettier, Lint on save, Jest, In dedicated conifg files, N

3. 생성된 프로젝트로 이동해
    `yarn serve`
    실행하여 웹브라우저에서 확인 (localhost:8080)


## Github 수동 배포
1. Github에 vue-devops 프로젝트 생성

2. 원격 저장소 설정 및 코드 푸시

3. Github Pages 배포 라이브러리 추가
    `yarn add gh-pages -d`

4. package.json에서 배포에 필요한 정보 추가
    
    ```
    "name": "vue-devops",
    "version": "0.1.0",
    "private": true,
    "homepage": "https://jodawoooon.github.io/vue-devops/",
    "scripts": {
        "serve": "vue-cli-service serve",
        "build": "vue-cli-service build",
        "predeploy": "vue-cli-service build",
        "deploy": "gh-pages -d dist",
        "clean": "gh-pages-clean",
        "test:unit": "vue-cli-service test:unit",
        "lint": "vue-cli-service lint"
    },
    ```
    
5. 배포용 publicPath 설정
    이 설정이 있어야 https://<github_id>.github.io/vue-devops에서 정상적으로 페이지 확인 가능

    vue.config.js 파일을 생성하여
    ```
    module.exports = {
        publicPath: "/vue-devops/",
        outputDir: "dist"
    };
    ```
    
6. 정적 파일을 githu에 푸시

    `yarn deploy`


## GitHub Action workflow로 배포 자동화
1. Github Actions 메뉴의 첫 화면에서 Simple workflow 파일(deploy.yml)작성 후 커밋한다

2. git pull하여 deploy.yml 내려받는다.

3. 수정 후 커밋&푸시 하면 자동 배포 완료
