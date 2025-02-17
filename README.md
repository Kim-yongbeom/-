# 프론트엔드 기술

## ```www.google.com```을 치면 생기는 일
![캡처](https://user-images.githubusercontent.com/89058117/174774721-b6162823-8a18-45fd-a2a2-1babcbf6fb5c.PNG)

```
1. 웹 브라우저가 HTTP를 사용해 DNS에게 입력된 도메인 주소를 요청
2. DNS기록에서 'www.google.com'에 매칭되는 IP주소 찾고 응답 (DNS는 도메인 이름과 IP 주소를 서로 변환하는 역할을 한다)
3. 웹 브라우저가 웹 서버에 IP주소를 이용해 index.html 문서 요청
4. 브라우저의 요청을 받은 서버는 페이지의 로직이나 데이터베이스 연동을 위해 WAS(미들웨어 역할)에 요청을 한다.
5. 작업 결과를 웹 서버로 전송
6. 서버는 브라우저에 html문서 결과 응답 후 내용 출력
```

## 브라우저 작동원리
<img width="701" alt="스크린샷 2022-05-11 오전 12 03 40" src="https://user-images.githubusercontent.com/89058117/167660451-2f21e802-766a-4cc8-b2e6-67a64aa1ad1a.png">

```
'DOM트리'와 '스타일 규칙'을 합쳐서 '렌더 트리'를 만든다.
'렌더 트리'는 DOM 요소를 기반으로 만들어지지만 완전히 대응하는 구조로 만들어 지지는 않는다.

'DOM트리'가 문서의 구조를 나타낸다면 '렌더 트리'는 문서의 시각적 구조를 나타낸다.
display: none 일 때 DOM에는 물론 존재하지만, 시각적으로는 없는 것이기 때문에 '렌더 트리'에는 할당되지 않는다.

float 또는 position 값이 absolute, fixed 일 때 DOM 문서의 순서과 상관없이 시각적으로 위치하는 요소의 경우는
'DOM트리'와 다른 위치의 '렌더 트리'에 할당한다.

Reflow(배치): 최초에 한번 실행이 되고, 이후에 요소들의 레이아웃에 변화가 생기면 다시 '렌더 트리'를 구성하는 것을 Reflow라고 한다.

Repaint(그리기): Reflow가 발생하면 Repaint도 발생, 레이아웃에 영향을 주지 않는 엘리먼트 변화(color, background-color)에서는 Reflow가 발생하지 않고 Repaint만 발생한다.

Reflow, Repaint를 줄여서 랜더링 최적화 시키는 법: https://seokzin.tistory.com/entry/JavaScript-%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%B5%9C%EC%A0%81%ED%99%94-Reflow%EC%99%80-Repaint
```

## HTML이 렌더링 중에 Javascript가 실행되면 렌더링이 멈추는 이유?
- 간략한 브라우저 렌더링 과정
``` DOM트리 + CSSOM트리 -> 렌더트리 -> 레이아웃 -> 페인트  ```
- 위의 브라우저 렌더링 과정 가운데 JavaScript가 실행되면 렌더링이 멈추게 된다.
- 이유: 자바스크립트가 DOM API 통해서 DOM트리를 변경시킬 수 있기 때문이다.
```
JS엔진과 렌더링 엔진은 직렬적으로 실행
즉, 위에서 부터 한줄한줄 내려가며 코드를 실행시키고, 한 엔진이 실행되면 다른 엔진은 실행 권한X.
만약 파싱이 중단되지 않으면 렌더트리가 다 구성되지 않았을 때 JS엔진이 DOM트리를 변경시킬 수 있다.
해결을 위해 async를 사용해 비동기적으로 동시에 진행되도록 만들어줌.

async의 역할은 자바스크립트 실행이 로드되면 바로 진행되며 이때 HTML파싱 중단.
```

## 프로세스와 스레드 차이
- 프로세스: 컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램
- 스레드: 프로세스 내에서 실행되는 여러 흐름의 단위

## 멀티 프로세스와 멀티 스레드 차이
- 멀티 프로세스: 하나의 응용프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 하나의 작업을 처리함
```
장점: 여러 개의 자식 프로세스 중 하나에 문제가 발생해도 크게 영향이 확산되지 않는다.
단점: 프로세스가 작업을 처리하는 과정에서 캐시 메모리 초기화 등 무거운 작업이 진행되어 많은 시간이 소모된다.
```
- 멀티 스레드: 하나의 응용프로그램을 여러 개의 스레드로 구성하여 각 스레드가 하나의 작업을 처리함
```
장점: 스레드는 프로세스 내의 Stack 영역을 제외한 모든 메모리를 공유해 통신 부담이 적고, 자원의 효율성이 좋다
단점: 디버깅이 까다롭다, 하나의 스레드에 문제가 생기면 전체 프로세스가 영향을 받는다
```

## 메모리 영역(힙, 스택 메모리 차이)
![캡처](https://user-images.githubusercontent.com/89058117/174586989-d0ab4988-aacf-426a-8e72-4742a3e7dcac.PNG)

- 스택
```
1. 정적 메모리 할당
2. 함수의 호출과 함께 할당되며, 함수의 호출이 완료되면 소멸
3. 메모리의 높은 주소에서 낮은 주소의 방향으로 할당

장점: 매우빠른 액세스, 변수를 명시적으로 할당 해제 할 필요가 없다.
단점: 메모리 크기 제한, 지역 변수만
```
- 힙
```
1. 동적 메모리 할당
2. 사용자에 의해 메모리 공간이 동적으로 할당되고 해제
3. 메모리의 낮은 주소에서 높은 주소의 방향으로 할당

장점: 변수는 전역적으로 액세스 할 수 있다. 메모리 크기 제한이 없다.
단점: 상대적으로 느린 액세스, 메모리를 관리해야 한다.
```

## 자바스크립트 불변성
- 원시 타입은 불변성을 가짐
- 참조 타입은 불변성을 가지지 않음

## 자바스크립트 원시 타입
- 숫자, 문자열, boolean, null, undefined 인 다섯가지 기본 타입

## 자바스크립트 참조 타입
- Object, Array

## 원시타입과 참조타입
- 원시 타입 -> 고정된 크기로 call stack 메모리에 저장, 실제 데이터가 변수에 할당
- 참조 타입 -> 데이터 크기가 정해지지 않고 call stack 메모리에 저장, 데이터의 값이 heap에 저장되며 변수에 heap 메모리의 주소값이 할당

## 불변성을 지켜야 하는 이유
- 값이 변할 때 원본 데이터가 변경되기에 이 원본 데이터를 참조하고 있는 다른 객체에서 예상치 못한 오류가 발생할 수 있다.
- 리액트에서 화면을 업데이트할 때 불변성을 지켜서 값을 이전 값과 비교해서 변경된 사항을 확인한 후 업데이트하기 때문이다.

## 불변성을 지키는 방법
- spread operator, map, filter, slice, reduce 와 같이 새로운 배열을 반환하는 메소드를 사용한다.

## 절차 지향 프로그래밍
- 일이 진행되는 순서대로 프로그래밍하는 방법
```
장점: 코드의 가독성이 좋음
단점: 유지보수 및 분석이 어려움
```

## 객체 지향 프로그래밍
- 모든 데이터를 객체로 취급하고, 객체가 처리 요청을 받았을 때, 객체 내부에 있는 기능을 사용해 처리하는 방법
```
특징: 1) 추상화: 공통적인 속성이나 기능을 묶어서 이름을 붙이는 것
      2) 캡슐화: 데이터를 은닉하고 데이터 기능을 노출시키지 않음
      3) 상속성: 상위 부모 객체의 속성과 특징을 하위 객체가 물려 받는 것
      4) 다형성: 같은 함수가 있어도 매개변수에 따라 각자 다른 일을 하는 것
      
장점: 코드의 재사용이 가능 (유지보수에 용이)
단점: 처리 속도가 상대적으로 느림
```

## 함수형 프로그래밍
- 외부의 영향을 받지 않는 함수를 사용해, 상태를 제어하기보단 빨리 처리하는데 초점을 둔 방법
```
장점: 객체지향 프로그래밍에 비해 코드 이해도와 가독성이 좋아짐
단점: 외부 데이터 혹은 내부 데이터의 상태를 조작할 수 없음
```

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
먼저 전역 컨텍스트 하나 생성 후, 함수 호출 시마다 컨텍스트가 생깁니다. 컨텍스트 생성 시 컨텍스트 안에 
변수객체[arguments(함수의 인자), variable(해당 스코프의 변수들)], scope chain(자신과 상위 스코프들의 변수객체), this가 생성됩니다.
컨텍스트 생성 후 함수가 실행되는데, 사용되는 변수들은 변수 객체 안에서 값을 찾고, 없다면 스코프 체인을 따라 올라가며 찾습니다.
함수 실행이 마무리되면 해당 컨텍스트는 사라집니다.(클로저 제외) 페이지가 종료되면 전역 컨텍스트가 사라집니다.
```

## 스코프, 스코프 체인, 렉시컬 스코프
- 전역 스코프: 코드 어디서든지 참조할 수 있다.
- 지역 스코프: 함수 코드 블록이 만든 스코프로 함수 자신과 하위 함수에서만 참조할 수 있다.
- 스코프 체인: 내부 함수는 외부 함수의 변수에 접근 가능해 변수를 찾기 위해 계속 상위 함수로 올라간다. 계속 범위를 넓히면서 찾는것.
- 렉시컬 스코프(정적 스코프): 자바스크립트는 렉시컬 스코프를 따르고, 함수를 어디서 호출하는지가 아니라 어디에 선언하였는지에 따라 결정된다. 호출x, 선언o 

## 호이스팅
- JavaScript에서 호이스팅(hoisting)이란, 
- 인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미합니다.
- 호이스팅을 설명할 땐 주로 "변수의 선언과 초기화를 분리한 후, 선언만 코드의 최상단으로 옮기는" 것으로 말하곤 합니다.
- 스코프 내부 어디서든 변수 선언은 최상위에서 선언된 것 처럼 행동
- var는 선언과 초기화가 동시에 일어나 호이스팅시 정상 작동, 그러나 초기엔 undefined
- let/const 는 호이스팅이 되지만 레퍼런스에러 발생
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
- this는 기본적으로 window이다.
- strict 모드에서는 undefined
```
var obj = {
  a: function() { console.log(this); },
};
obj.a(); // obj
```
- 객체 메서드 a 안의 this는 객체를 가리킨다.
```
var a2 = obj.a;
a2(); // window
```
- 호출하는 함수가 객체의 메서드인지 그냥 함수인지가 중요하다. 
- a2는 obj.a를 꺼내온 것이기 때문에 더 이상 obj의 메서드가 아니다.
```
var obj2 = { c: 'd' };
function b() {
  console.log(this);
}
b(); // Window
b.bind(obj2).call(); // obj2
b.call(obj2); // obj2 
b.apply(obj2); // obj2
```
- 명시적으로 this를 바꾸는 함수 메서드 bind, call, apply를 사용하면 this가 객체를 가리킨다.
```
$('div').on('click', function() {
  console.log(this);
});
```
- this는 클릭한 div이다. 이런건 어쩔 수 없이 외워야함
```
$('div').on('click', function() {
  console.log(this); // <div>
  function inner() {
    console.log('inner', this); // inner Window
  }
  inner();
});
```
- inner 함수 호출 시 this는 window이다.
```
$('div').on('click', function() {
  console.log(this); // <div>
  const inner = () => {
    console.log('inner', this); // inner <div>
  }
  inner();
});
```
- 해결하기 위해 ES6부터는 화살표 함수를 사용해 window 대신 상위 함수의 this를 가져온다.
- this는 객체 메서드, bind, call, apply, new 일 때 바뀐다.

## map 메서드
- map() 메서드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환합니다.
```
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

## slice 메서드
- slice() 메서드는 어떤 배열의 begin부터 end까지(end 미포함)에 대한 얕은 복사본을 새로운 배열 객체로 반환합니다. 원본 배열은 바뀌지 않습니다.
```
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]
```

## 얕은 복사
```
const obj1 = { a: 1, b: 2};
const obj2 = obj1;
console.log( obj1 === obj2 ); // true
```
- 위의 예시처럼 객체를 직접 대입하는 경우 참조에 의한 할당이 이루어지므로 둘은 같은 데이터(주소)를 가지고 있다. 이것이 얕은 복사이다.

## 깊은 복사
```
const obj1 = { a:1, b:2 };
const obj2 = { ...obj };
obj2.a = 100;
console.log( obj1 === obj2 ) // false
console.log( obj1.a ) // 1
```
- ...(spread) 연산자를 통해 { }안에 obj1의 속성을 복사하여 obj2에 할당하였다. obj1과 obj2는 다른 주소를 갖게되었다. (그러나 딱, 1 depth 까지만)

## 콜백 함수
- 다른 함수의 인자로써 이용되는 함수.
- 어떤 이벤트에 의해 호출되어지는 함수.

## Promise, async await
- Promise: 비동기 작업의 단위
- Promise의 예외처리: .catch()
- async await: Promise를 좀 더 편하게 사용하게 해줌
- async await의 예외처리: try & catch
- await은 Promise가 처리될 때 까지 기다리게해줌

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
```
function run() {
  console.log('동작');
}
console.log('시작');
setTimeout(run, 3000);
console.log('끝');
```

![캡처](https://user-images.githubusercontent.com/89058117/174711160-104e534a-101f-414f-82e0-bef9a95ee259.PNG)
- setTimeout이 호출되고 지워지면서 백그라운드로 run함수와 함께 3초 타이머를 보낸다. 3초 후 백그라운드에서 태스크 큐에 run함수를 보냄.

![캡처](https://user-images.githubusercontent.com/89058117/174711576-b0c8b91f-5204-47eb-9d84-44721cee9a5f.PNG)
- 이벤트 루프는 항상 대기하고 있다가 호출 스택이 비워지면 태스크 큐에서 함수를 하나씩 호출 스택으로 밀어 올린다.

![캡처](https://user-images.githubusercontent.com/89058117/174711709-e29e16ae-111d-40ec-b7a2-648925a2b641.PNG)
- run함수가 실행되고 호출 스택에서 지워지게 된다. 이벤트 루프는 태스크 큐에 새로운 함수가 들어올 때까지 대기한다.

```
- setTimeout 0초도 마찬가지입니다. setTimeout을 하는 순간 백그라운드를 거쳐 태스크 큐로 run함수가 이동해 console.log()가 먼저 찍힌다.
- 호출 스택에 함수들이 가득차 있다면 3초보다 더 걸릴 수 있다.
- 콜 스택이 가득 차 있다면 setTimeout 0을 사용해 극복할 수 있다.
- 백그라운드를 사용하는 작업은 타이머 외에도 ajax요청, 이벤트 리스너, FileReader 등이 있다.
- 자바스크립트 기본 제공 메소드 중 콜백 함수를 사용하는 것들은 백그라운드를 사용하는 경우가 많다.

- 태스크 큐 말고도 마이크로태스크 큐가 존재하고 Promise의 동작 방식과 연관이 있다.
- 백그라운드의 ```setTimeout()```의 콜백함수가 태스크 큐에 들어가고, ```Promise```의 콜백함수가 마이크로태스크 큐에 들어간다.
- 이벤트 루프는 마이크로태스크 큐의 모든 태스크들을 처리한 다음,태스크 큐의 태스크들을 처리한다. 따라서 ```Promise```의 콜백함수가 ```setTimeout()```의 콜백함수보다 먼저 처리된다.
```

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
- 출처: https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%9D%B4%ED%84%B0%EB%9F%AC%EB%B8%94-%EC%9D%B4%ED%84%B0%EB%A0%88%EC%9D%B4%ED%84%B0-%F0%9F%92%AF%EC%99%84%EB%B2%BD-%EC%9D%B4%ED%95%B4
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

## CORS
- 브라우저에서 보안적인 이유로 HTTP요청들을 제한한다.
- 지정된 도메인 외부에 있는 자원에 대한 접근을 통제하는 브라우저 메커니즘

## [HTML/CSS] display 속성 알아보기 (display:none과 visibility:hidden 차이)
- display:none은 화면 상 어떤 영역을 차지하지 않고 완전히 삭제된 것처럼 보이게 한다.
- visibility: hidden은 해당 요소가 보이지 않을 뿐 요소가 존재하는 영역은 확실히 보이게 된다.





