# Day5 (2021.11.17)

_정리 : 도토리_

## 객체

- 원시값을 제외한 거의 모든 것이 객체다!

- 객체는 '프로퍼티'의 집합이다.

- 객체 생성 방법은?  
  객체리터럴 `{...}` 외에 함수를 사용하여 생성한다.

- 프로퍼티 동적 생성과 delete
  <br>
  <br>

## 얕은 복사와 깊은 복사

<p align="center">
  <img src="https://github.com/moonyerim2/Javascript-Deep-Dive/blob/main/%EC%96%95%EC%9D%80%EB%B3%B5%EC%82%AC%EA%B9%8A%EC%9D%80%EB%B3%B5%EC%82%AC.PNG?raw=true" width="450px" height="150px"/></p>

- 얕은 복사(shallow copy)란?

  객체를 복사할 때 참조에 의한 할당이 이루어지므로 원본과 같은 메모리 주소를 갖게 되고 이것이 얕은 복사이다.
  그러므로 한 변수의 데이터를 변경하면 다른 변수의 데이터의 값도 함께 변경 된다.
  즉, 한 데이터를 공유하고 있는 것이다. (원본===카피 -> true)

- 깊은 복사(deep copy)란?

  참조가 아닌 값을 그대로 복사하지만, 같은 값을 가지는 별개의 메모리 공간을 갖는다.
  그러므로 한 객체 값의 변경이 다른 객체 값의 변경에 영향을 주지 않는다. (원본===카피 ->false)
  <br>
  <br>

## 원시값과 객체의 Copy

<p align="center">
  <img src="https://github.com/moonyerim2/Javascript-Deep-Dive/blob/main/%EC%9B%90%EC%8B%9C%EA%B0%92%EA%B0%9D%EC%B2%B4copy.PNG?raw=true" width="750px" height="400px"/></p>

원시값은 깊은 복사를 하지만 객체는 얕은 복사을 기반으로 한다.
그리하여 객체는 한 데이터의 공유가 아니라 똑같은 구조의 객체를 하나 더 생성하여 따로 사용하고자 할 때 깊은 복사가 필요하다.
<br>
<br>

객체의 깊은 복사 방법은 크게 4가지가 있다.

- spread(...)
- Object.assign()
- JSON.parse(JSON.stringify(obj));
- lodash의 cloneDeep 사용(Node.js 환경)

spread(...)와 Object.assign()은 중첩되어 있으면 얕은 복사, 중첩되어 있지 않으면 깊은 복사가 이루어진다.
depth 1까지는 깊은 복사가 가능하지만 depth 2부터는 얕은 복사가 되므로 중첩된 객체는 문법의 재귀적 사용을 통해 깊은 복사가 가능하다.
<br>
<br>

### [배열과 객체의 복사]

- 배열의 복사

  1. 얕은복사

     - 그냥 할당(const arrB = arrA)
     - spread(...) (depth 2부터)
     - slice()  (depth 2부터)

  2. 깊은복사
     - 스프레드를 재귀적/여러번 사용

- 객체의 복사
  1. 얕은 복사
     - 그냥 할당
     - spread(...) (depth 2부터)
     - Object.assign() (depth 2부터)
  2. 깊은 복사
     - JSON.parse(JSON.stringify(오브젝트));
     - lodash의 cloneDeep 사용(Node.js 환경)

## 결론

자바스크립트에서는 값에 의한 전달만 있고, 사실상 참조에 의한 전달은 없다.
참조에 의한 전달을 뜯어보면, 결국 그것도 값(값이 다른 값에 대한 메모리주소였을 뿐)에 의한 전달이기 때문이다.

그렇다면 왜 자바스크립트에서 진정한 깊은 복사를 수행할 수 없을까?

그 이유는 자바스크립트 내부적으로 그렇게 모델링 되어있지 않기 때문이다.
그렇기 때문에 일부 라이브러리들은 사용자의 요구를 채워주기 위해 다소 낮은 퍼포먼스를 띠더라도 정확하게 모든 요소를 복사하는 메소드를 구현해 놓았다.

그러나 역시 가장 베스트는, 깊은 복사를 하기 전에 과연 깊은 복사를 무리하면서까지 해야하는지 아키텍쳐 관점에서 다시 한 번 생각해봄이 좋지 않을까 하고 생각한다.
