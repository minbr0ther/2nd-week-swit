<p align="middle">
  <img src="https://user-images.githubusercontent.com/24728385/158543304-028bcb34-2339-45f6-aa3e-dee6bb77ff1a.png" />
</p>

<h1 align="middle">Redux로 상태관리를 하는 메신저 Swit</h1>

1. React, Redux 구현
2. 메신저 삭제, 답장, 추가 기능 구현
<br/>

# 🔗 배포
[https://infallible-panini-19ee47.netlify.app/](https://infallible-panini-19ee47.netlify.app/)

[![Netlify Status](https://api.netlify.com/api/v1/badges/4cdb7c60-5f99-420f-9f10-5420389e3332/deploy-status)](https://app.netlify.com/sites/infallible-panini-19ee47/deploys)

<br/>

# ⚙️ 설치 및 시작하는 법

```
$ git clone https://github.com/pre-onboarding-course-team-6/2nd-week-swit

$ cd 2nd-week-swit

$ npm install

$ npm run start
```
<br/>

# 🏹 과제 구현 목록 및 담당
> ✨ 이슈 해결 및 추가 구현사항 안내 [Notion🔗](https://minbr0ther.notion.site/Swit-014d3ba9d4734f0eb67a7d1254364612)

<br/>

## 로그인

- [x]  `prompt`로 이름을 입력받아서 진행

<br/>

## 레이아웃 (일반적인 메신저 레이아웃)

- [x]  대화목록은 상단에 위치하며, 입력창은 하단에 있습니다.
- [x]  입력창 과는 별도로 대화목록만 스크롤 가능합니다.
- 입력창
    - [x]  왼쪽에는 입력란이 있습니다.
    - [x]  오른쪽에는 보내기 버튼이 존재합니다.
- 메시지
    - [x]  프로필 이미지는 원형으로 왼쪽에 보입니다.
        - [x]  본인의 프로필 이미지는 입력받은 이름의 첫글자를 보여줍니다
        - [x]  배경색은 CSS 하시는분 마음대로
    - [x]  오른쪽 컨텐츠 영역 상단에는 이름과 보낸 날짜 
    하단에는 보낸 메시지의 내용이 출력됩니다.
    - [x]  메시지의 가장 오른쪽에는 삭제 버튼과 답장 버튼이 존재합니다.

<br/>

## 기능

- 데이터 (Redux)
    - [x]  메시지의 데이터 모델에는 userId, userName, profileImage, content, date 등이 있습니다.
    
- 입력창
    - [x]  엔터키로 전송할 수 있습니다. 입력시 전송버튼은 즉시 활성화 됩니다.
    - [x]  컨텐츠를 입력하지 않으면 전송할 수 없습니다.
    - [x]  입력란은 멀티라인으로 입력하고
        - [x]  메시지에서의 출력도 그대로 출력됩니다.
    
- 대화목록(현명, 무길)
    - [x]  메시지의 정렬은 과거 부터 최신 순으로 정렬됩니다.
    - [x]  메시지를 보낼때 대화목록은 항상 가장 아래로 스크롤 됩니다.
        - [x]  scrollY ? 조절
    - [x]  대화목록은 미리 생성된 데이터로 3명이 5건의 메시지를 주고 받는 내용이 출력됩니다.
        - [x]  default value
    
- 메시지 (현명, 무길)
    - [x]  내가 전송한 메시지의 경우 이름 옆에 * 문자가 출력됩니다.
    - [x]  보낸 날짜의 경우 yyyy-mm-dd hh:MM:ss 포멧으로 출력됩니다. (사용자의 시간대로 출력) - (민형님, 선명님)
    - [x]  답장을 클릭하면 "사용자 이름\n" + "메시지 내용\n" + "(회신)\n" 문자가 입력창에 자동으로 삽입됩니다. (\n 개행, 입력창에 내용이 존재할때는 입력된 내용 앞에 입력됩니다.
    - [x]  삭제 버튼을 클릭하면 "*** 메시지를 삭제하시겠습니까?" 라는 메시지가 출력되며 응답시 삭제됩니다.
        - [x]  confirm, 혹시라도 추가 구현하고 싶다면 모달

<br/>

# 🤯 이슈 해결

- [https://stackoverflow.com/questions/62259351/react-redux-error-default-parameters-should-be-last-default-param-last](https://stackoverflow.com/questions/62259351/react-redux-error-default-parameters-should-be-last-default-param-last) : 두시간 삽질,, eslint & redux 충돌

<br/>

- Uncaught TypeError: Cannot read properties of undefined (reading 'name') : useSelector 에러
    
    ```tsx
    const name = useSelector((state) => state.logInReducer.user.name);
    // combineReducers를 사용하면,
    // state.{사용하는 리듀서}.{state 내부접근} 순으로 해야한다.
    // 그런데 state.{state 내부접근} 이렇게 접근해서 오류가 있었다.
    ```

<br/>  

- npm run start시 iframe 강제생성 오류: package.json에 다음 코드를 추가
    
    ```jsx
    "resolutions": {
        "react-error-overlay": "6.0.9"
      },
    "devDependencies": {
        "react-error-overlay": "6.0.9"
      },
    "scripts": {
        "preinstall": "npx npm-force-resolutions"
      }
    ```
    
<br/>

- onSubmit 새로고침 되는 현상
    - button 말고 form에 onSubmit 속성 달아줘야 refresh 현상 없어짐
    
    ```tsx
    <form onSubmit={onSubmit}>
    ```
<br/>

- 입력창에서 shift + enter 하면 개행, enter는 전송
    
    ```tsx
    <MessageInput
      type="text"
      placeholder="Enter message"
      name="message"
      onChange={onChange}
      onKeyDown={handleKeyPress} 
       // onKeyUp -> onKeyDown 이슈 해결! 
    />
    
    const handleKeyPress = (e) => {
      // shift + ender 하면 return, 개행 적용
      if (e.key === 'Enter' && e.shiftKey) {
        return;
      }
    
      // 그냥 enter 입력하면 
      if (e.keyCode === 13) {
        e.preventDefault();
    
        // 메시지 입력을 하지 않았을때 enter누르면 반환
    		if (text.length === 0) return;
    
        onSubmit(e);
      }
    };
    ```

<br/>

1. 로그인 cancel시 null 뜨는 현상
        
    ```tsx
    useEffect(() => {
      let userInput;
      while (true) {
        userInput = prompt('사용자 이름을 입력해주세요.');
    
    		// 입력받은 값이 있으면 while문 탈출
        if (userInput !== null && userInput.length > 0) break;
      }
      dispatch(logIn(userInput));
      alert(`반갑습니다 ${userInput}님 😀`);
    }, []);
    ```
    
<br/> 

# 🏗 전체적인 개발 순서

## 0. 프로젝트 세팅

- ~~CRA~~
- ~~ESLint, Prettier (+ TypeScript)~~
- ~~Redux, Styled-components~~
- ~~README.md~~
- ~~절대경로 세팅 src/jsconfig.json~~
- ~~components 나누기~~
- ~~git repo 생성~~
    - slack git subscribe pre-onboarding-course-team-6/{레포이름}

## 1. REDUX 세팅

- 초기 상태 - 메세지 5개 보여주기
- 메세지 리스트, 접속자

## 2. 컴포넌트 기능 구현

- 컴포넌트간 구별을 위한 inline style (border) 등만 하기
- 개발후 pull request 날리기

## 3. CSS 스타일링


## 3. 리팩토링


<br/>

# 🏗 프로젝트 구조

```
📦src
 ┣ 📂actions             // 액셔 타입 정의
 ┃ ┗ 📜types.js
 ┣ 📂components
 ┃ ┣ 📂ChannelToolbar    // 상단바 header
 ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┗ 📜styled.js
 ┃ ┣ 📂Input             // 입력창 컴포넌트
 ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┗ 📜styled.js
 ┃ ┣ 📂Message           // 메세지 컴포넌트
 ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┗ 📜styled.js
 ┃ ┗ 📂MessageList       // 메세지 리스트 컴포넌트
 ┃ ┃ ┣ 📜index.jsx
 ┃ ┃ ┗ 📜styled.js
 ┣ 📂reducers            // 리듀서
 ┃ ┣ 📜index.js
 ┃ ┣ 📜initState.js
 ┃ ┗ 📜reducer.js
 ┣ 📂styles
 ┃ ┣ 📜globalStyles.js
 ┃ ┗ 📜styled.js
 ┣ 📜App.jsx
 ┣ 📜index.jsx
 ┗ 📜store.js

```
<br/>

## ✅ Git - Commit Message Convention [🔗](https://webruden.tistory.com/486)

- feat : 새로운 기능 추가 (a new feature)
- fix : 버그 수정 (a bug fix)
- docs : 문서 수정 (changes to documentation)
- style : 코드 포맷팅, 세미콜론 누락, 코드 변경이 없는 경우 (formatting, missing semi colons, etc; no code change)
- refactor : 코드 리펙토링 (refactoring production code)
- test : 테스트 코드, 리펙토링 테스트 코드 추가 (adding tests, refactoring test; no production code change)
- chore : 빌드 업무 수정, 패키지 매니저 수정 (updating build tasks, package manager configs, etc; no production code change)
<br/>

## 👨‍👨‍👦‍👦 팀구성원 소개

| [<img src="https://github.com/minbr0ther.png" width="100px">](https://github.com/minbr0ther) | [<img src="https://github.com/BGM-109.png" width="100px">](https://github.com/BGM-109) | [<img src="https://github.com/wiseeee.png" width="100px">](https://github.com/wiseeee) | [<img src="https://github.com/gilmujjang.png" width="100px">](https://github.com/gilmujjang) |
| :------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------------------: |
|                        [22_01 정민형](https://github.com/minbr0ther)                         |                       [22_01 김선명](https://github.com/BGM-109)                       |                       [22_01 이현명](https://github.com/wiseeee)                       |                        [22_01 민무길](https://github.com/gilmujjang)                         |
