# localStorage vs sessionStorage

:heavy_check_mark: 학습내용:

- 개요
  - browser storage, web storage
  - localStorage, sessionStorage의 공통적인 장점
  - storage의 필요성과 용도
- localStorage/sessionStorage의 차이점과 장단점
- 사용 구문
- 특이사항(forEach)

<br>

## 1. 개요

- Browser Storage : 브라우저에 정보를 캐시하거나 저장할 수 있는 공간.
- Web storage : HTML5에 도입된 저장소이며 JS로 접근할 수 있다.

local, sessionStorage는 key/value를 로컬에 저장하기 좋은 툴이다. 사용자 인증으로 쿠키 대신 사용하기도 한다.
두 tool의 공통적인 장점은 다음과 같다.

- 데이터는 로컬에만 저장되고 서버에서 읽을 수 없다. 즉 쿠키의 단점인 보안문제가 없다.
- 많은 데이터를 저장할 수 있다. (대부분의 브라우저에서 10MB, 모바일에서는 2.5MB)
- 간단하게 사용 가능하다.
- 모든 최신 브라우저에서 지원된다.

localStorage와 sessionStorage는 거의 동일하고, 같은 API를 사용한다.

storage의 필요성에 대해 잠시 적어보자면, 웹사이트가 데이터에 의존하는 경우에 사용하기 좋다. 성능에 관련한 문제인데, 사용자의 브라우저에 로컬로 저장된 데이터는 즉시 사용이 가능하고 반면 원격으로 저장된 데이터는 서버에서 사용자에게 전송된다. 데이터 요청 후 서버 응답에 시간이 걸리므로 빠른 액세스를 위해선 브라우저에 데이터를 저장하는 게 좋다. Browser storage는 아래와 같이 다양한 용도로 사용된다.

- 이전 세션의 데이터 유지, 장바구니 내용 저장, 투두 리스트 항목, 이전 로그인 기록
- 페이지 렌더링에 영향을 주는 사이트 기본 설정의 개인화
- 사용자 지정 UI
- 네트워크 연결이 오프라인 상태거나, 사이트가 빨리 로드되어야 하는 경우

이제 localStorage와 sessionStorage의 차이점을 알아보자.

<br />

## 1. localStorage와 sessionStorage의 차이점

개념적인 차이점은 '얼마나 오래 보존되느냐'다.

#### 1-1. localStorage

데이터 영속성을 갖고 있다. 즉, 사용자가 직접 개발자 도구를 통해 데이터를 삭제하거나 웹 애플리케이션에서 삭제하지 않으면 계속해서 브라우저에 남아있다. 이 점은 당연히 같은 컴퓨터에서 같은 브라우저를 사용할 때만 해당한다.

<b>장점</b>

- 데이터에 만료날짜가 없다.
- 저장 용량이 10MB로 크다.
- 데이터가 서버로 전송되지 않는다.

<b>단점</b>

- 데이터가 일반 텍스트이므로 설계상 안전하지 않다.
- 데이터 유형은 오로지 문자열이므로 serialize가 필요하다.
- 데이터를 클라이언트 측에서만 읽을 수 있다. (잘 활용하면 장점이 된다.)

#### 1-2. sessionStorage

웹페이지의 탭 혹은 창이 닫히는 등 세션이 끝날 때 저장된 데이터가 지워진다.

<br>

## 3. 구문

localStorage, sessionStorage의 구문을 간략하게 정리해보겠다.

| Methods        | localStorage                                | sessionStorage                                  |
| -------------- | ------------------------------------------- | ----------------------------------------------- |
| 항목 생성      | localStorage.setItem(key, 'Value')          | sessionStorage.setItem(key, 'Value')            |
| 읽기           | localStorage.getItem(key), localStorage.key | sessionStorage.getItem(key), sessionStorage.key |
| 업데이트       | localStorage.setItem(key, 'New Value')      | sessionStorage.setItem(key, 'New Value')        |
| 삭제           | localStorage.removeItem(key)                | sessionStorage.removeItem(key)                  |
| 항목 모두 삭제 | localStorage.clear()                        | sessionStorage.clear()                          |

local, session만 구분해줄 뿐 구문이 완전히 같습니다. 두 tool 모두 JSON 문자열만 저장할 수 있는데, 아래와 같은 코드로 자주 사용한다.

```
//객체 및 배열을 저장할 때 문자열로 변환해야 유효한 값이 된다.
localStorage.setItem(key, JSON.stringify(Obj));

//문자열화 된 값을 읽고 반환할 때 사용한다.
const item = JSON.parse(localStorage.getItem(key));
```

<br>

## 4. 특이사항

localStorage 값을 전부 확인하기 위해 forEach 메소드를 사용했으나 작동하지 않았다. 알고보니 localStorage와 sessioinStorage 객체는 forEach를 지원하지 않는다. 따라서 항목을 조회하려면 for문으로 반복해야 한다.

```
if (localStorage.length > 0) {
    for (let i = 0 ; i < localStorage.length ; i++>) {
        let key = localStorage.key(i);
        let val = localStorage.key;
        // let val = localStorage.getItem(key);
        console.log(key, value)
    }
}
```

위와 같이 간단하게 local/sessionStorage의 항목을 전부 조회할 수 있다.

<br>

## Reference

- JAVASCRIPT.INFO(localStorage와 sessionStorage) : https://ko.javascript.info/localstorage
- Digital Ocean (Introduction to localStorage and sessionStorage) : https://www.digitalocean.com/community/tutorials/js-introduction-localstorage-sessionstorage#step-1-understanding-localstorage-vs-sessionstorage
- XENONSTACK (Local Storage vs Session Storage vs Cookie) : https://www.xenonstack.com/insights/local-vs-session-storage-vs-cookie
