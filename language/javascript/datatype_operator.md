# 자바스크립트 데이터 타입
## 종류
### Primitive Types
- `Undefined`
- `Null`
- `Boolean`
- `String`
- `Number`

### Reference Types
- `Object`
> primitive types를 제외한 나머지 모든 타입

<br ><br >

- 숫자를 표현하는데 `Number type` 하나만 존재
- 소수 표현에 부동소수점 사용

<br >

- String 표현에 Double(`""`) / Single(`''`) 둘 다 사용 가능 
- String이 참조타입이 아닌 기본 타입

## 특징
### Dynamic typing
> 변수를 선언할 때 타입을 지정하지 않아도 된다   
> - 코드 실행 시에 `문맥`에 따라 데이터 타입이 결정됨!

<br >

**어떻게 가능할까?😶**   
실행 시점의 문맥에 따라 변수를 Wrapper Class로 감싼다.
Wrapper 객체는 사용이 끝나면 시스템이 회수 해 간다


---
<br ><br >

# 연산자
## `==` vs `===`
`==` , `!=`
- 값을 비교
- 경우에 따라 자동 형변환이 발생


`===` , `!==`
- 값과 타입 모두 비교
- 자동 형변환 발생 x

> 정확한 비교를 위해서는 `==`, `!=` 보다는 `===` , `!==` 사용 권장

<br >

## `&&` , `||` 연산자
```javascript

var x = (1 && true && "str" && {}) // {}

var x = (1 || true || "str" || {}) // 1

var x = (1 && true || "str" || {}) // true

```

**`가장 왼쪽이 표현식부터 평가 된다`**

**`&&`연산자**
- 왼쪽 표현식부터 순서대로 하나씩 확인해 모두 true인지 검사
- 표현식의 처리 결과가 false 경우 해당 시점의 `표현식을 리턴`
- 모두 `true`이면 마지막 표현식이 리턴

**`||`연산자**
- 왼쪽 표현식부터 순서대로 하나씩 확인해 모두 false인지 검사
- 표현식의 처리 결과가 true 경우 해당 시점의 `표현식을 리턴`
- 모두 `false`이면 마지막 표현식이 리턴

