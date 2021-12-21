# Globals 



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









