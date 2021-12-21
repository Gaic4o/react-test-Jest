# Globals 



``` javascript
describe(name, fn) 
```

여러 관련 테스트를 그룹화 하는 블록을 만듭니다.
예로 들면 지갑이라는 함수를 만들고,
지갑 함수 안에 만원이 있는지, 백원이 있는 지 True/False 검사 할 수 있습니다.

``` javascript
const 지갑 = {
    만원 = true,
    백원 = false, 
}

describe('나의 지갑', () => {
    test('지갑에 만원이 있습니까?', () => {
        expect(지갑.만원).toBeTruthy(); // true === true => true 
    });

    test('지갑에 백원이 있습니까?', () => {
        expect(지갑.백원).toBeFalsy(); // false === false => false 
    })
})
```



``` javascript
describe.only(name, fn) 
```

- 테스트 파일에서 test 할 것들을 실행하고 싶을 떄 넣어주는 함수 입니다.
  
``` javascript
test(name, fn, timeout) 
```


describe.only 하나의 설명 블록만 실행하면 됩니다.

``` javascript
describe.only('나는 지갑을 가지고 테스트 할 것이 1가지 밖에 없어서 only로 하나만 테스트 하자', () => {
    test('지갑에 만원이 있을까?', () => {
        expect(지갑.만원).toBeTruthy(); // true == true => true 
    })

    test('지갑에 백원이 있을까?', () => {
        expect(지갑.백원).toBeFalsy(); // false === false => true 
    })
});
```



``` javascript
describe.only.each(table)(name, fn) 
```

describe.only.each -> 데이터 기반 테스트의 특정 테스트 모음만 실행하려는 경우 사용 합니다.








``` javascript
test.concurrent(name, fn, timeout) 
```

test.concurrent 테스트 코드들을 동시에 실행 합니다. (비동기 함수를 사용 할 떄 주로 사용하는 것 같습니다.)

``` javascript
test.concurrent('이 값이 2일 까요?', async () => {
    expect(2 + 1).toBe(3); // true 
});

test.concurrent('이 값은 5일 까요?', async () => {
    expect(3 + 2).toBe(5); // true 
})
```





``` javascript
afterAll(fn, timeout) 
beforeAll(fn, timeout) // 이 파일은 테스트가 실행 되기전 함수를 실행 됩니다. 
``` 

모든 파일 -> 테스트 코드가 다 완료된 후 최종적으로 afterAll 함수가 실행이 됩니다.


``` javascript
const globalDatabase = makeGlobalDatabase();

function cleanUpDatabase(db) {
    db.cleanUp(); 
}

afterAll(() => {
    clearnUpDatabase(globalDatabase); 
});

test('can find things', () => {
    return globalDatabase.find(....)
})

test('can insert a thing', () => {
    return globalDatabase.insert(....)
})
```








``` javascript
afterEach(fn, timeout)
beforeEach(fn, timeout) // 이 파일의 각 테스트가 실행되기 전 함수를 실행합니다. 
```

이 함수도 마찬가지로 All 은 모든 테스트 코드였지만, AfterEach 는 파일의 각 테스트가 완료 된 후 실행이 됩니다.


``` javascript
const globalDatabase = makeGlobalDatabase();

function cleanUpDatabase(db) {
    db.cleanUp();
}

afterEach(() => {
    cleanUpDatabase(globalDatabase); 
});

test('can find things', () => {
    return globalDatabase.find...
})
```





``` javascript
test.concurrent.each(table)(name, fn, timeout) 
```

test.concurrent.each 는 다른 데이터로 동일한 테스트를 계속 복제하는 경우 사용 합니다.
test.each 테스트를 한 번 작성 후 데이터를 전달 할 수 있도록 하면 `테스트`가 모두 `비동기적`으로 실행됩니다. 

test.concurrent.each 두 가지 API 로 사용 할 수 있습니다. 

``` javascript
test.concurrent.each(table)(name, fn, timeout) 
```

table: 각 행 `Array`에 대한 테스트 fn 에 전달된 인수가 있는 배열의 수 입니다.

name: String 테스트 블록의 제목 입니다. 
    %p : pretty-format.
    %s : String.
    %d : Number.
    %i : Integer.
    %f : Floating point value.
    %j : JSON. 
    %o : Object.
    %# : Index of the test case.
    %% : single percent sign ('%')

fn : Function 실행 할 테스트는 각 행의 매개변수를 함수 인수로 꼭 함수 이며 비동기여야 합니다.

``` javascript
test.concurrent.each([
    ['민수', '지수'],
    ['지수', '민수'],
    ['기성', '수현'],
])('.add(%s, %s)', async (a, b, expected) => {
    expect(a + b).toBe(expected); 
})
```





1. test.concurrent.each`table`(name, fn, timeout) 
   
`table` : `Trgged Template Literal` -> ${value} 구문을 사용.
`name` : 테스트 제목, 태그가 지정된 템플릿 표현식에서 테스트 제목을 데이터를 삽입하는 데 String 또는 $variable 합니다.
`fn` : Function 실행할 테스트, 테스트 데이터 객체를 수신할 함수, 비동기 함수여야 합니다.






``` javascript
test.each(table)(name, fn, timeout)
```

`test.each` 다른 데이터로 동일 테스트를 계속 복제하는 경우 사용 합니다.
`test.each` 테스트를 한 번 작성 후 데이터를 전달 할 수 있습니다.


``` javascript
test.each(table)(name, fn, timeout) 
```

table : 각 행 `Array` 에 대한 테스트 `fn` 에 전달된 인수가 있는 배열 입니다.
name: String 테스트 블록의 제목 입니다. 
    %p : pretty-format.
    %s : String.
    %d : Number.
    %i : Integer.
    %f : Floating point value.
    %j : JSON. 
    %o : Object.
    %# : Index of the test case.
    %% : single percent sign ('%')

fn : Function 실행 할 테스트는 각 행의 매개변수를 함수 인수로 꼭 함수 이며 비동기여야 합니다.
    


``` javascript
test.each([
    {a: 3, b: 5, expected: 8},
    {a: 2, b: 3, expected: 5},
    {a: 1, b: 5, expected: 6},
])('.add($a, $b)', ({a, b, expected}) => {
    expect(a + b).toBe(expected); 
}
```



``` javascript
test.only(name, fn, timeout) 
```

또한 별칭 : it.only(name, fn, timeout) 및 fit(name, fn, timeout) 

-> 큰 테스트 파일을 디버깅 할 때 하위 집합만 실행하려는 경우가 많습니다.
    .only 하여 해당 테스트 파일에서 실행할 유일 테스트를 지정 할 수 있습니다.

``` javascript
test.only('민수 집', () => {
    expect(민수함수()).toBeGreaterThan(0);
});

test('민수는 지금 지갑에 얼마가 있을까', () => {
    expect(민수지갑()).toBe(0);
})
```


``` javascript
test.todo(name) 
```

todo 함수는 -> 테스트 작성을 계획 할 떄 사용 합니다.

이 테스트는 마지막에 요약 출력에서 강조 표시되므로 아직 수행해야 하는 테스트의 수를 알 수 있습니다.

``` javascript
const 민수 = (a, b) => a + b;
test.todo('a+b 한 값을 이제 곱 해야 합니다.'); 
```