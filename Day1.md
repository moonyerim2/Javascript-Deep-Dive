- ## 변수

  - 변수 호이스팅이란?

  - undefined

    변수를 선언하고 값을 할당하지 않으면 undefined라는 값이 할당되어 초기화 된다.

- ## 표현식과 문

  - 리터럴이란?

  - 토큰 (Token)

  - 표현식과 문의 차이

- ## 데이터 타입

  - 데이터 타입의 개수는?

  - 원시타입 vs 객체 타입?

  - 동적 타입 언어란?

  - 객체의 복사

    - 깊은 복사: 원시 자료형과는 달리 객체를 복사할 때는 참조 방식이 쓰인다. 참조란 '메모리 주소(address)'를 저장하는 것을 말한다.

    ```js
    let car = { color: "red" };
    let secondCar = car; //참조 복사
    car.wheels = 4;
    console.log(car === secondCar); //true
    ```

    - 얕은 복사: 객체 복사본을 만드는 방법이다. - Object.assign();

    ```js
    const secondCar = Object.assign({}, car);
    ```

  - 배열의 복사

    - 얕은복사

    ```js
    1. .slice()
    2. const arrB=[].concat(arrA);
    3. const arrB=[...arrA];
    ```

  - 변수 사용시 주의사항

    1. 변수는 최소한으로 사용한다.
    2. 변수의 유효 범위(스코프)는 최대한 좁게 만든다.
    3. 전역 변수는 최대한 사용하지 않는다.
    4. 상수를 사용해 값의 변경을 억제한다.(const)
    5. 변수의 목적이나 의미를 파악할 수 있도록 네이밍한다.
