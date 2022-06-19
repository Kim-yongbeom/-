# 프론트엔드 기술

## 브라우저 작동원리
<img width="701" alt="스크린샷 2022-05-11 오전 12 03 40" src="https://user-images.githubusercontent.com/89058117/167660451-2f21e802-766a-4cc8-b2e6-67a64aa1ad1a.png">


## 자바스크립트의 특징
- 자바스크립트는 객체 기반의 스크립트 언어이다.
- 자바스크립트는 동적이며, 타입을 명시할 필요가 없는 인터프리터 언어이다.
- 자바스크립트는 객체 지향형 프로그래밍과 함수형 프로그래밍을 모두 표현할 수 있다.
```
C언어와 같은 언어는 소스 파일을 작성한 후, 해당 파일을 컴파일(compile)하여 사용자가 실행할 수 있는 실행 파일(.exe)로 만들어 사용합니다.
하지만 인터프리터 언어는 이러한 컴파일 작업을 거치지 않고, 소스 코드를 바로 실행할 수 있는 언어를 의미합니다.
자바스크립트는 웹 브라우저에 포함된 자바스크립트 인터프리터가 소스 코드를 직접 해석하여 바로 실행해 줍니다.
```

## 변수 설정
- var는 함수 스코프이다. 함수 스코프는 함수 내에서 선언된 변수만 지역 변수가 된다
- let, const는 블록 스코프이다. 블록 스코프는 모든 코드 블록에서 선언된 변수는 코드 블록 내에서만 유효하며 외부에서는 접근할 수 없다.

## 자바스크립트 실행 컨텍스트
```
https://junilhwang.github.io/TIL/Javascript/Domain/Execution-Context/#_5-this
```

## 호이스팅
- JavaScript에서 호이스팅(hoisting)이란, 
- 인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미합니다.
- 호이스팅을 설명할 땐 주로 "변수의 선언과 초기화를 분리한 후, 선언만 코드의 최상단으로 옮기는" 것으로 말하곤 합니다.
- 스코프 내부 어디서든 변수 선언은 최상위에서 선언된 것 처럼 행동
- var는 선언과 초기화가 동시에 일어나 호이스팅시 정상 작동, 그러나 초기엔 undefined
- let은 선언과 초기화가 따로 일어난다 호이스팅되면서 선언 단계가 이뤄지지만 초기화 단계는 실제 코드에 도달했을때 되기때문에 레퍼런스 에러가 발생한다.
- const는 선언, 초기화, 할당이 동시에 이뤄진다.
```
catName("클로이");

function catName(name) {
  console.log("제 고양이의 이름은 " + name + "입니다");
}

/*
결과: "제 고양이의 이름은 클로이입니다"
*/
```
- 함수 호출이 함수 자체보다 앞서 존재하지만, 그럼에도 불구하고 이 코드 역시 동작합니다. 이것이 JavaScript에서 실행 맥락이 동작하는 방식입니다.

## 클로저
```
클로저는 내부함수와 밀접한 관계를 가지고 있다
내부함수는 외부함수의 지역변수에 접근 할 수 있는데
외부함수의 실행이 끝나서 외부함수가 소멸된 이후에도
내부함수가 외부함수의 변수에 접근 할 수 있다 
```
![캡처](https://user-images.githubusercontent.com/89058117/168408006-84bcde48-be70-4918-ac87-6f18330619d3.PNG)

## margin, padding 차이
- 각 요소간의 보더 간격을 margin , 보더와 요소와의 간격을 padding 이라고 한다.
![캡처](https://user-images.githubusercontent.com/89058117/168428188-73c2f0e0-3578-4764-a73b-7c7baa0e1178.PNG)

## GET, POST 차이
- GET 은 클라이언트에서 서버로 어떠한 리소스로 부터 정보를 요청하기 위해 사용되는 메서드이다. 
- POST는 클라이언트에서 서버로 리소스를 생성하거나 업데이트하기 위해 데이터를 보낼 때 사용 되는 메서드다.

## this
- 자바스크립트의 this는 해당 함수 호출 방식에 따라 this에 바인딩되는 객체가 달라진다.

## 브라우저 저장소 차이점 (LocalStorage, SessionStorage)
```
SessionStorage는 데이터가 지속적으로 보관되지 않는다. 이는 마치 브라우저 기반 세션 쿠키와 그 성질이 비슷한데, 현재 페이지가 브라우징되고 있는 브라우저 컨텍스트 내에서만 데이터가 유지된다.

LocalStorage는 브라우저를 종료해도 데이터는 보관되어 다음번 접속에도 그 데이터를 사용할 수 있는 반면, SessionStorage는 브라우저가 종료되면 데이터도 같이 지워진다. 즉, 브라우저가 종료되면 SessionStorage도 삭제된다는 것이다.
```

## 쿠키와 세션
- 쿠키와 세션 사용 이유: HTTP 프로토콜의 약점을 보완하기 위해서 사용한다.
- 쿠키
```
HTTP의 일종으로 사용자가 어떠한 웹 사이트를 방문할 경우,
그 사이트가 사용하고 있는 서버에서 사용자의 컴퓨터에 저장하는 작은 기록 정보 파일이다.
HTTP에서 클라이언트의 상태 정보를 클라이언트의 PC에 저장하였다가 필요시 정보를 참조하거나 재사용할 수 있다.
```
- 세션
```
일정 시간 동안 같은 사용자(브라우저)로부터 들어오는 일련의 요구를 하나의 상태로 보고, 그 상태를 유지시키는 기술이다.
여기서 일정 시간은 방문자가 웹 브라우저를 통해 웹 서버에 접속한 시점부터 웹 브라우저를 종료하여 연결을 끝내는 시점을 말한다.
즉, 방문자가 웹 서버에 접속해 있는 상태를 하나의 단위로 보고 그것을 세션이라고 한다.
```
- 쿠키와 세션의 차이
```
쿠키와 세션은 비슷한 역할을 한다. 그 이유는 세션도 결국 쿠키를 사용하기 때문이다.
둘의 차이점은 쿠키는 서버의 자원을 전혀 사용하지 않으며, 세션은 서버의 자원을 사용한다.
보안 면에서 세션이 더 우수하다. 속도는 쿠키가 우수하다. (이유: 세션은 정보가 서버에 있기 때문에 보안은 좋지만 속도는 느리다, 쿠키는 쿠키에 정보가 있기 때문에 속도가 빠르다)
```

## 캐시
- 캐시는 웹 페이지 요소를 저장하기 위한 임시 저장소이다.
- 쿠키/세션은 정보를 저장하기 위해 사용한다.
- 캐시는 웹 페이지를 빠르게 렌더링 할 수 있도록 도와준다.
- 쿠키/세션은 사용자의 인증을 도와준다.

## 자바스크립트는 싱글스레드 언어이지만 실제 사용시 멀티스레드 언어처럼 어떻게 사용하는가?
- 싱글스레드 방식은 한 번에 하나의 테스트만 처리할 수 있다는 것을 의미한다.
- 하지만 브라우저가 동작하는 것을 살펴보면 많은 테스크가 동시에 처리되는 것처럼 느껴진다.
- ex) html 요소가 애니메이션 효과를 통해 움직이면서 이벤트를 처리하기도 하고, http요청을 통해 서버로부터 데이터를 가지고 오면서 렌더링하기도 한다.
- 이처럼 자바스크립트의 동시성을 지원하는 것이 이벤트루프
- 이벤트루프는 브라우저에 내장되어 있는 기능 중에 하나
![캡처](https://user-images.githubusercontent.com/89058117/168584234-2d6e9306-c679-4226-a0f5-6ce88fcec639.PNG)
- Memory Heap: 선언된 변수들이 메모리 할당이 이뤄지는 곳이다.
- Call Stack: 코드가 실행될 때 호출 스택이 쌓이는 곳이다.(호출된 함수가 call stack에 push된다) 자바스크립트 엔진은 단 하나의 콜 스택을 사용하기 때문에 실행 중인 실행 컨택스트가 종료되어 콜 스택에서 제거되기 전까지는 다른 어떤 테스크도 실행되지 않는다.
- 자바스크립트 언어 자체가 비동기 동작을 지원하는 것은 아니다. 자바스크립트 엔진은 단순히 테스크가 요청되면 콜스택을 통해 요청작업을 순차적으로 실행할 뿐이다.
- 브라우저의 구조
![캡처](https://user-images.githubusercontent.com/89058117/168584689-bcc9a94c-6c25-4d2b-ad53-2f669101c81b.PNG)
- 비동기 처리에서 소스코드의 평가와 실행을 제외한 모든 처리는 자바스크립트 엔진을 구동하는 환경인 브라우저 또는 node.js가 담담한다.
- 실제로 자바스크립트가 구동되는 환경인 웹 브라우저에는 여러 개의 Thread가 사용된다.
- 결론
```
자바스크립트는 Single Thread 프로그래밍 언어라 한 번에 하나씩 밖에 실행할 수 없지만, 
Web API, Callback Queue, Event Loop 덕분에 멀티 스레드처럼 동시성을 지니고 있다.
```

## 이벤트 루프
- 이벤트 루프란 자바스크립트 엔진이 아닌, 구동하는 환경(브라우저, 노드)에서 가지고 있는 장치이다. 콜 스택과 태스크 큐(= 콜백 큐)를 감시하며, 콜 스택이 비어있을 경우에 태스크 큐에서 태스크(=콜백함수)를 가져와 콜 스택에 넣어 실행시키는 기능을 한다.
- 태스크 큐 말고도 마이크로태스크 큐가 존재하고 Promise의 동작 방식과 연관이 있다.
- Web API의 ```setTimeout()```의 콜백함수가 태스크 큐에 들어가고, ```Promise```의 콜백함수가 마이크로태스크 큐에 들어간다.
- 이벤트 루프는 마이크로태스크 큐의 모든 태스크들을 처리한 다음,태스크 큐의 태스크들을 처리한다. 따라서 ```Promise```의 콜백함수가 ```setTimeout()```의 콜백함수보다 먼저 처리된다.

## 이벤트 버블링
- 이벤트 버블링은 특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위의 화면 요소들로 전달되는 특성을 의미한다.
- 버블링 방지하기 위해 event.stopPropagation() 사용
```
function logEvent(event) {
	event.stopPropagation();
}
```

## 이벤트 캡쳐
- 이벤트 캡쳐는 이벤트 버블링과 반대 방향으로 진행되는 이벤트 전파 방식이다.
- 이벤트 캡쳐를 사용하기 위해 addEventListener() API에서 옵션 객체에 capture: true를 넣어주면 된다.
- 캡쳐도 event.stopPropagation()을 사용해서 멈출 수 있다.

## 이터러블(iterable)
- 이터러블은 자료를 반복할 수 있는 객체를 말한다.
- 흔히 쓰는 배열 역시 이터러블 객체이다.
- 이터레이터를 리턴하는 ```[Symbol.iterator]()```메서드를 가진 객체이다.
- 배열의 경우 Array.prototype의 Symbol.iterator를 상속받기 때문에 이터러블이다.

## 이터레이터(iterator)
- {value: 값, done: true/false} 형태의 이터레이터 객체를 리턴하는 next() 메서드를 가진 객체이다.
- next 메서드로 순환 할 수 있는 객체이다.
- ```[Symbol.iterator]()```안에 정의 되어있다.
```
const arr = [1,2,3]; //arr는 그냥 평범한 배열
const iter = arr[Symbol.iterator]();

iter.next()
//>{value:1,done: false}

iter.next()
//>{value:2, done: false},

iter.next()
//{value:3, done: false}

iter.next()
//{value: undefined, done: true}
```

## 이터러블 프로토콜과 이터레이터 프로토콜
- 이터러블을 [for ...of], [전개 연산자], [비구조화] ..등, 이터러블이나 이터레이터 프로토콜을 따르는 연산자들과 함께 동작하도록 하는 약속된 규약을 의미한다. 그래서 이터러블이란 이터러블 규약을 따르는 객체이다.

## 제너레이터
- ES6에서 도입된 제너레이터 함수는 이터러블을 생성하는 함수이다.
- 제너레이터 함수를 사용하면 이터레이션 프로토콜을 준수해 이터러블을 생성하는 방식보다 간편하게 이터러블을 구현할 수 있다.
- 제너레이터 함수는 비동기 처리에 유용하게 사용된다.
- 제너레이터 함수는 function* 키워드로 선언한다. 그리고 하나 이상의 yield 문을 포함한다.
```
// 제너레이터 함수 선언문
function* genDecFunc() {
  yield 1;
}
```

## HTML이 렌더링 중에 Javascript가 실행되면 렌더링이 멈추는 이유?
- 









