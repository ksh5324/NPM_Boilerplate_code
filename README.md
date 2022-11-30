# NPM 보일러플레이트 코드

이 보일러플레이트 코드는 다음과 같은 상황을 대비하여 제작되었습니다.  
하나의 그룹에서 여러가지의 프로젝트가 제작되고 이는 곳 재사용 코드가 등장한다는 것입니다.

이때 여러가지의 해결법이 존재하긴 합니다. 모노레포르를 통해 로직을 따로 관리할 수 도 있지만  
npm에 package를 배포시켜놓고 다운 받는 방식으로도 사용됩니다.

로직을 배포시키기 위해 세팅이 필요한데 이를 위한 보일러 플레이트 코드입니다.

## default package

기본적으로 대구소프트웨어고등학교의 학생들을 대상으로 제작하였기에 react, react-dom, styled-components가 기본 값으로 세팅되어있습니다. 그러나 만일 다른 패키지가 필요하다면 설치, 필요없다면 삭제를 통해 수정 할 수 있습니다.

또한 언어는 typescript 기반입니다.

## 구조

src안에 모든 로직이 존재해야하며, index.ts는 실제 배포될 코드를 모으는 파일로 내보내는 코드만 존재해야합니다.

```ts
export * from "./math";
```

## 명령어

build-publish를 통해 빌드 및 npm package에 배포를 합니다.

```json
"scripts": {
    "build:clear": "rm -rf build",
    "build": "yarn build:clear && tsc && node ./esbuild.config.js",
    "build-publish": "npm run build && npm version patch && node setupPackage.js && cd build && npm publish"
  },
```
