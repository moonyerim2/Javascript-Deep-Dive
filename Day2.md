# Day2 (2021.11.13)
___정리 : Marco___
## undefined와 null의 차이점
- undefined
  - undefined는 선언은 되었지만 값이 할당된 적이 없는 변수에 접근하거나, 존재하지 않는 객체 프로퍼티에 접근할 경우 반횐되는 값이다.
- null
  - null은 보통 객체 타입의 특수한 값, 즉 어떠한 객체도 나타내지 않는 값으로 취급된다. null은 다른 모든 값들과 구분되는 고유한 값이다.  어떤 변수의 값을 초기화 하고 싶을 경우엔 null을 사용한다.

## null에 대한 typeof 연산자의 반환값은 null이 아니다.
- 일단 typeof 연산자는 피연산자의 데이터 타입을 7가지 문자열(string, number, boolean, undefined, symbol, object, function) 중 하나로 반환한다.
- typeof null의 반환값은 object이다. typeof array도 object이다. 둘 다 정확히 해당 type을 반환하지 않고 큰 틀에서 object라고 반환된다. 
- 따라서 null과 array의 type을 정확히 확인하려면,
  -  null의 경우, `=== null`과 같은 일치연산자를 사용하여 boolean을 통해 null type을 체크하고
  -  array의 경우, `Array.isArray()` 메서드를 사용하여 반환된 boolean을 통해 array type을 체크한다.

## 정확한 비교 결과를 반환하는 Object.is 메서드 
- Object.is 메서드 : ES6에서 도입된 이 메서드는 다음과 같이 예측 가능한 정확한 비교 결과를 반환한다.
- +0과 -0은 자바스크립트상 서로 다르다. 그런데 일치비교연산자는 이를 같다고 잘못 평가한다. 이에 대한 대안으로 Object.is()메서드를 사용하면 정확한 평가 결과인 false가 반환된다
- NaN와 NaN는 같은 값임에도 불구하고 일치비교연산자가 다르다고 잘못 평가하는데, 마찬가지로 NaN 끼리 같은지 확인하기 위해서 Object.is()메서드를 사용한다.
```js
-0 === +0; //true
Object.is(-0, +0); //false
NaN === NaN; //false
Object.is(NaN, NaN); true
```js
  - NaN은 자신과 일치하지 않는 유일한 값이다. 따라서 숫자가 NaN인지 조사하려면 빌트인 함수 isNaN을 사용한다.
```js
isNaN(NaN); // true
```
 
## 거짓 같은 값, 참 같은 값
```js
//거짓 같은 값, 아래 8개의 경우 모두 조건문 내에서 false로 평가된다.
if (false)
if (null)
if (undefined)
if (0)
if (-0)
if (0n)
if (NaN)
if ("")
```

```js
//참 같은 값, true 평가되는 경우이다.
if (true)
if ({})
if ([])
if (42)
if ("0")
if ("false")
if (new Date())
if (-42)
if (12n)
if (3.14)
if (-3.14)
if (Infinity)
if (-Infinity)
```

## 논리 연산자(||, &&)를 사용한 단축평가
- 논리 연산자를 사용한 단축평가 : 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환한다. 이를 단축평가라 한다. 단축평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것을 말한다
  - 논리 연산자의 결과가 불리언이 아닐 수 있다.
```js
console.log(false && 'Dog') //false
console.log(null && false) //null
console.log(false && null) //false
```
- 논리곱(&&) 연산자의 경우, 좌항의 평가 결과가 false(null, '', undefined도 falsy)인 경우 우항을 보지 않더라도 논리곱 연산의 결과가 당연히 false이기 때문에, 
  - `논리 연산의 결과를 결정하는 피연산자를` 타입 변환하지 않고 그대로 반환한다는 것이 특징이다. 그래서 좌항 피연산자로 null이 있고 논리곱을 한 경우에는, 그 결정적 피연산자인 null이 반환된다. 
- 논리곱 연사자를 조건문에서 사용할 경우, `if(함수&&변수)`보다는 `if(변수&&함수)`와 같은 순서로 쓰는 것이 메모리상 효율적이다.

## 옵셔널 체이닝 연산자, null 병합 연산자
- 옵셔널 체이닝 연산자(`?.`) : ES11에 도입된 옵셔널 체이닝 연산자 ?.는 좌항의 연산자가 null 또는 undefined인 경우 undefined를 반환하고, 그렇지 않으면 우항의 프로퍼티 참조를 이어간다. 옵셔널 체이닝 연산자 ?.는 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때 유용하다. 옵셔널 체이닝 연산자 ?.가 도입되기 이전에는 논리 연산자 &&를 사용한 단축 평가를 통해 변수가 null 또는 undefined인지 확인했다.
  - 옵셔널 체이닝 연산자를 사용하면 프로퍼티가 없는 중첩 객체를 에러 없이 안전하게 접근할 수 있다는 것이 장점이고 의의이다. 다만, 남용하지 말고 `왼쪽 평가대상이 없어도 괜찮은 경우에만 선택적으로 사용`하는 것이 적절하다.
  - 옵셔널 체이닝 연산자(`?.`)는 읽기나 삭제하기에는 사용할 수 있지만 쓰기에는 사용할 수 없다.
  - `obj?.prop` – obj가 존재하면 obj.prop을 반환하고, 그렇지 않으면 undefined를 반환함
  - `obj?.[prop]` – obj가 존재하면 obj[prop]을 반환하고, 그렇지 않으면 undefined를 반환함
  - `obj?.method()` – obj가 존재하면 obj.method()를 호출하고, 그렇지 않으면 undefined를 반환함
- null 병합 연산자(`??`) : ES11에서 도입된 null 병합 연산자 ??는 좌항의 피연산자가 null 또는 undefined인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환한다. null 병합 연산자 ??는 변수에 기본값을 설정할 때 유용하다. null 병합 연산자 ??가 도입되기 이전에는 논리 연산자 ||를 사용한 단축 평가를 통해 변수에 기본값을 설정했다.
```js
var foo = null ?? 'default string';
var foo2 = null || 'default string';
console.log(foo); //'default string' 
console.log(foo2); //'default string'
```

## 증감연산자 위치에 따라 다른 효과
- 피연산자 앞에 위치한 전위 증가/감소 연산자는 먼저 피연자의 값을 증가/감소시킨 후, 다른 연산을 수행한다.
- 피연산자 뒤에 위치한 후위 증가/감소 연산자는 먼저 다른 연산을 수행한 후, 피연산자의 값을 증가/감소시킨다.
```js
let a = 1
let b = 1

console.log(++a) //2
console.log(b++) //1
console.log(b) //2
``` 



