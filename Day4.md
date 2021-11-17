# 제너레이터

## 제너레이터 함수 정의
```javascript
    function* genDecFunc() {
        yield 1;
    }
```
### 주의
- 애스터리스크(*)의 위치는 function 키워드와 함수 이름 사이에 있기만 하면 된다.
- 화살표 함수로는 정의할 수 없다.
- new 연산자와 함께 생성자 함수로 호출할 수 없다.

## 제너레이터 객체
- 제너레이터 함수는 제너레이터 객체를 생성해 반환한다.
- 제너레이터 객체는 이터레이터이다.
- 제너레이터 객체는 next 메서드를 가진다.
- next 메서드는 result객체를 반환한다.
- result객체는 value와 done 프로퍼티를 가진다.
```javascript
    const generator = genFunc();

    console.log(generator.next()); //리절트 객체 {value: 1, done: false}
```

## yield 키워드와 next 메서드
- generator.next()는 다음 yield 표현식까지만 코드를 실행한다.
- yield 키워드는 함수의 실행을 일시 중지시킨다.
- yield 키워드는 키워드 뒤에 오는 표현식의 평가 결과를 제너레이터 함수 호출자에게 반환한다.
