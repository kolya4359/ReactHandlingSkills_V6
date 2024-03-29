# 블로그 제작에 필요한 정보

## 라우트 컴포넌트

- LoginPage.js : 로그인
- RegisterPage.js : 회원가입
- WritePage.js : 글쓰기
- PostPage.js : 포스트 읽기
- PostListPage.js : 포스트 목록

## 프록시(proxy) 설정

현재 백엔드 서버는 4000 포트, 리액트 개발 서버는 3000 포트로 열려 있기 때문에 별도의 설정 없이 API를 호출하려고 하면 오류가 발생한다. 이 오류를 CORS(Cross Origin Request) 오류라고 부른다. 네트워크 요청을 할 때 주소가 다른 경우에 발생한다. 이 오류를 해결하려면 다른 주소에서도 API를 호출할 수 있도록 서버 쪽 코드를 수정해야 한다. 그런데 최종적으로 프로젝트를 완성하고 나면 결국 리액트 앱도 같은 호스트에서 제공할 것이기 때문에 이러한 설정을 하는 것은 불필요하다.  
그 대신 프록시(proxy)라는 기능을 사용할 것이다. 웹팩 개발 서버에서 지원하는 기능인데, 개발 서버로 요청하는 API들을 우리가 프록시로 정해 둔 서버로 그대로 전달해 주고 그 응답을 웹 애플리케이션에서 사용할 수 있게 해준다.

```js
// package.json
...
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "proxy": "http://localhost:4000/"
}
```

이제 리액트 애플리케이션에서 client.get('/api/posts')를 하면, 웹팩 개발 서버가 프록시 역할을 해서 http://localhost:4000/api/posts에 대신 요청한 뒤 결과물을 응답해 준다.

## 회원 가입 시 발생하는 에러 처리

회원가입은 에러 처리가 조금 까다롭다. 다음 상황에 대한 에러를 모두 처리해 주어야 한다.

- username, password, passwordConfirm 중 하나라도 비어 있을 때
- password와 passwordConfirm 값이 일치하지 않을 때
- username이 중복될 때

## 글쓰기 기능 구현 순서

- UI를 만든다.
- 기능을 구현한다.
- Quill 에디터를 사용했는데 Quill 에디터는 일반 input, textarea과 다르기 때문에 onChange와 value 값을 사용하여 상태를 관리할 수 없다.  
  그래서 에디터에서 값이 바뀔 때 리덕스 스토어에 값을 넣는 작업을 우선 구현하고, 리덕스 스토어의 값이 바뀔 때 에디터 값이 바뀌게 하는 작업을 추가로 구현해준다.
- 글쓰기 API 연동

## PostViewer UI 준비하기

서버에서 데이터를 받아 오기 전에 먼저 UI를 완성한다. 구현할 UI는 다음 정보를 보여 준다.

- 포스트 제목
- 태그
- 작성자 계정명
- 제목
- 작성된 시간
- 내용

## 수정 / 삭제 버튼 구현

작성자에게만 나타나는 수정 / 삭제 버튼을 만든다.  
PostViewer 컴포넌트 안에 나타나도록 만드는데 PostViewer에서 직접 렌더링하면, 나중에 PostActionButtons에 props를 전달할 때 무조건 PostViewer를 거쳐서 전달해야 한다.  
정작 PostViewer 내부에서는 사용하지 않지만 내부의 컴포넌트에서 필요하기 때문에 한 번 거쳐 전달하는 것은 불편하다.  
그래서 props를 JSX 형태로 받아 와서 렌더링한다.

```js
// example
<PostViewer
  post={post}
  loading={loading}
  error={error}
  actionButtons={<PostActionButtons onEdit={onEdit} onRemove={onRemove} />}
/>
```

이 방법은 굳이 컨테이너 컴포넌트를 새로 만들 필요 없이 기존 PostViewerContainer에서 필요한 로직을 작성하면 된다.
