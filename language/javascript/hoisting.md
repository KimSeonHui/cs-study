# 호이스팅
인터프리터가 코드 실행하기 전 함수, 변수, 클래스 , import 선언문을 해당 스코프의 맨 위로 이동 시키는 과정
- 자바스크립트 엔진은 코드 실행 전 **모든 선언(var, let, const, function, class)을 스코프에 등록**
- 코드 실행 전 이미 `변수 선언 / 함수 선언`이 저장되어 있기 때문에 선언문보다 참조 / 호출이 먼저 나와도 오류 없이 동작함


## 변수 호이스팅(var, let , const )
- `let` , `const`,  `class` 를 이용한 선언문을 호이스팅이 발생하지 않는 것처럼 동작
- `temporal dead zone`이 선언 이전의 변수 사용을 엄격히 금지
- 따라서 `var` 외 키워드로 선언된 변수를 선언문 이전에 참조하면 `ReferenceError(참조 에러)`가 발생

>**Temporal Dead Zone(TDZ)**?    
> 일시적 사각지대     
> 스코프의 시작 지점 ~ 초기화 시작 지점까지의 구간

<br /><br />

### 변수 생성과 호이스팅
변수는 3단계에 걸쳐 생성된다

**1단계 : 선언 단계(Declaration phase)**
- 변수를 실행 컨텍스트의 변수 객체에 등록
- 변수 객체는 스코프가 참조하는 대상이 된다

**2단계 : 초기화 단계(Initinalization phase)**
- 변수 객체에 등록된 변수를 위한 공간을 메모리에 확보
- 이 단계에서 변수는 undefined로 초기화 됨

**3단계 : 할당 단계(Assignment phase)**
- undefined로 초기화된 변수에 실제 값을 할당


<br />

**왜 오류가 날까?**
- `var` 키워드는 선언과 함께 `undefined`로 초기화 되어 메모리에 저장
- 선언 단계와 초기화 단계가 한 번에 이뤄짐
- 변수 선언문 이전에 변수에 접근해도 스코프에 변수가 존재하기 때문에 에러 발생 X
- `undefined` 반환, 변수 할당문에 도달하면 값이 할당됨

<br />

- `let`, `const`는 초기화 되지 않은 상태로 선언만 메모리에 저장되기 때문에 초기화 되지 않아 변수를 참조할 수 없어 참조 에러가 발생됨
- 선언 단계와 초기화 단계가 분리되어 진행
- 초기화 단계는 변수 선언문에 도달 했을 때 이뤄지기 때문에 초기화 이전에 변수에 접근하려고 하면 참조 에러 발생

<br /><br />

## 예시
```javascript
// 호이스팅 때문에 선언이 끌어올려져서 오류 안남.
console.log(text); // (선언 + 초기화 된 상태) :: undefined
text = 'Hanamon!'; // (선언 + 초기화 + 할당 된 상태)
var text;
console.log(text); // Hanamon
```



```javascript
// 호이스팅 때문에 선언이 끌어올려졌지만 초기화 안된 상태에서 참조해서 오류 남.
console.log(text); // (선언 된 상태, 초기화(메모리 공간 확보와 undefined로 초기화) 안되서 참조 불가능 -> 에러남)
let text; // 여기서 초기화 단계가 실행됨
```

```bash
Uncaught SyntaxError: Identifier 'text' has already been declared
```

<br />

### 함수 호이스팅
```javascript
foo1(); // 함수 선언문에서는 호이스팅 일어난다.
foo2(); // 함수 표현식이라서 변수 호이스팅이 일어나 TypeError 발생

function foo1() { // 함수 선언문 :: 함수 선언, 초기화 , 할당이 한 번에 이뤄짐
  console.log('Hello');
}

var foo2 = function() { // 함수 표현식 
  console.log('world');
}
```
