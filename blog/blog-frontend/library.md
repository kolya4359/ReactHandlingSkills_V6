# 사용한 라이브러리

- styled-components: CSS in JS 기술을 사용하여 스타일을 설정한다. 이 기술은 JS 안에 CSS를 작성하는 것을 의미한다.

- redux: 가장 많이 사용하는 **리액트 상태관리 라이브러리**이다.

  - 리덕스를 사용하면 컴포넌트의 상태 업데이트 관련 로직을 다른 파일로 분리시켜서 더욱 효율적으로 관리할 수 있다.
  - 컴포넌트끼리 똑같은 상태를 공유해야 할 때도 여러 컴포넌트를 거치지 않고 손쉽게 상태 값을 전달하거나 업데이트할 수 있다.
  - 프로젝트의 규모가 클 경우에는 리덕스를 사용하는 편이 좋다.
    - 코드의 유지 보수성도 높여주고 작업 효율도 극대화 해 주기 때문이다.
    - 개발자 도구도 지원하며, 미들웨어라는 기능을 제공하여 비동기 작업을 훨씬 효율적으로 관리할 수 있게 해준다.

- react-redux: 리액트 환경에서 리덕스를 사용할 수 있도록 도움을 주는 라이브러리이다.

- redux-actions: 액션 생성함수를 더 짧은 코드로 작성할 수 있게 해준다.

  - 리듀서를 작성할 때 switch문이 아닌 handleActions라는 함수를 사용할 수 있게 해준다.

- immer: 리액트에서 불변성을 유지하는 코드를 작성하기 쉽게 해주는 라이브러리.

- redux-devtools-extension: 크롬 개발자도구에서 redux 도구를 사용할 수 있게 해주는 라이브러리.

- axios: 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리 이다.

- redux-sage: Action을 모니터링하고 있다가, 특정 Action이 발생하게 되면 이에 따라 특정 작업을 하는 방식으로 사용한다. 이때 특정 작업이란, 특정 JavaScript를 실행하는 것일수도 있고, 다른 Action을 Dispatch 하는 것 일수도 있고, 현재 State를 불러오는 것 일수도 있다.