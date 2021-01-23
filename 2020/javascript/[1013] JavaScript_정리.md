[toc]

## 1013_workshop

# ECMAScript

## 1. 변수와 식별자

### 01.1 식별자

> 변수명은 식별자라고 불리며 특별 규칙을 따릅니다.

- 반드시 문자, 달러, _ 로 시작해야 한다. 숫자로 시작할 수 없다.(`-` 도 사용 불가능)
- 대소문자를 구분한다. 클래스명이 아니라면 시작 단어는 대문자 사용을 지양해야 한다.
- 예약어도 사용 불가능하다. (class, const, let, var, await, case ... )

#### 식별자 작성 스타일

- 기본적으로 camelCase로 작성한다. (lowcaseUppercase)

  ```javascript
  // 숫자, 문자, 불린
  let dog
  let babyCat
  
  // 배열 - 배열은 복수형으로 작성한다
  let animals
  
  // 함수
  function getPropertyName () {}
  
  // 이벤트 핸들러 - 이벤트 핸들러는 `on`으로 시작한다
  // 우리는 직접적으로 사용하지 않을 것이지만 알아두기
  function onclick () {}
  function onKeyDown () {}
  
  // 불린 반환 함수 - 리턴 값이 true, false - `is`로 시작한다
  function isauthenticated () {}
  ```

  

- PascalCase로 작성되는 경우 - 클래스, 생성자

  ```javascript
  // class 때만 대문자로 시작?
  class User {
      information(option) {
          this.name = option.name
      }
  }
  
  const people = new User({
      name: '홍길동',
  })
  ```



- 대문자 스네이크 케이스 (SNAKE_CASE)

  - 값이 변하지 않는다는 것을 알린다.

  ```javascript
  const API_KEY = 'api_key'
  const PI = '3.14......'
  ```

  

### 01.2 변수

#### let(변수) : 값을 재할당 할 수 있는 변수를 선언하는 키워드

```javascript
let x = 1
x = 3
```

- 선언은 단 한번만 가능하다. (개발자도구 콘솔창에서는 편의를 위해 가능하지만 코드상에서는 불가능!!)

```javascript
let x = 3
let x = 2
```



- 유효 범위가 블록을 기준으로 작성이 된다.

- 블록 유효 번위란 -> `if`, `for` 등등 {} 내부를 가리킨다.

  ```javascript
  let x = 1
  
  if (x == 1) {
      let x = 2
      console.log(x)
  }
  console.log(x)
  ```

  

#### const(상수) : 재할당도 재선언도 불가능하다.

- 값이 변하지 않는 상수를 선언하는 키워드

```javascript
const x = 4
x = 3
console.log(4)

const foo = {}
foo.bar = 4
console.log(foo)
console.lof(foo.bar)
```



- 상수를 선언할 때는, 반드시 값을 초기화 해줘야 한다.

```javascript
// 불가능
const a

// 반드시 값을 초기화 해주어야 한다.
const a = 3
```



- let과 같이 블록 유효 범위를 가진다.

```javascript
const num = 3

if (num == 3) {
    const num = 4
    console.log(num)
}
console.log(num)
```



|          | const |  let  |
| :------: | :---: | :---: |
|  재할당  |   x   |   o   |
|  재선언  |   x   |   x   |
| 유효범위 | block | block |



#### var(변수) : ES6 이전에 사용하던 변수 선언 방식

- 재할당도 되고, 재선언도 된다.
- 예기치 못한 상황을 발생 시킬 수 있으므로 **절대 사용하지 않는다!!!!!!!!!!!**

```javascript
var x = 3
var x = 2
console.log(x)
```



- 함수 유효 범위를 가진다.

```javascript
var x = 33
let y = 11

if (x == 33) {
    var x = 22
    let y = 1
    console.log(x)
    console.log(y)
}
console.log(x)
console.log(y)

>> 22 1 22 11 뜬다..
>> 밑에서 선언해버리면 위의 코드를 덮어씌움.
```



#### 정리

| const(defalt) | let         | var            |
| ------------- | ----------- | -------------- |
| 재할당 불가   | 재할당 가능 | 재할당 가능    |
| 재선언 불가   | 재선언 불가 | 재선언 가능    |
| block scope   | block scope | function scope |





### 01.3 Hoisting

- `var` 로 선언한 변수가 선언 이전에도 참조될 수 있는 현상.
- hoisting은 우리가 활용하는 기술이 아니고 <u>피해야하는 상황.</u>
- python에서는 밑의 코드처럼 작성하면 오류가 나지만 자바스크립트에서는 작동이 된다.

```javascript
console.log(name)

var name = '홍길동'
```

- 자바스크립트 코드 실행하면 다음과 같이 이해한다.

```javascript
var name
console.log(name)

var name = '홍길동'
```



- 그러므로 let과 const로 작성해야함!

- let(값을 초기화 안해줘도 됨) 으로 작성 했을 시 
- const(값변경 불가능하기 때문에 초기화해주고 작성)

```javascript
console.log(name)

let name = '홍길동'
// const name = '홍길동'
```





## 2. 타입과 연산자

### 02.1 Primitive(원시값, 원시 자료형) 타입

#### Number

```javascript
const a = 1
const b = -13
const c = 3.14
const d = 2.99e3
const e = Infinity
const f = -Infinity
const g = NaN

console.log(a, b, c, d, e, f, g)
```

- 파이썬에서는 type으로 알아보고 자바스크립트에서는  `console.log(typeof NaN)`



#### String

```js
const sentence1 = '문자열'
const sentence2 = '문자열'

console.log(sentence1)
console.log(sentence2)
```

- 문자열 간의 덧셈이 가능하다

```js
const firstName = '가영'
const lastName = '신'

const fullName = fistName + lastName

console.log(fullName)
```

- escape sequence

```js
const hello = "안녕 \n 하세요"

console.log(hello)
```



- Template Literal (밑에보다는 여기에 더 집중!)
- `` (backtick) 쓰기

```js
const name = '홍길동'

const sayHello = `${name}이 인사합니다.`
console.log(sayHello)
```

- ``(backtick) 안에서는 escape sequence를 사용할 수 없다
- 내가 줄바꿈 직접 해주기

```js
const nextSentence = `안녕
하세요`

console.log(nextSentence)
```



#### Boolean

- 소문자

```js
true
false
```



#### Empty Value

- 값이 존재하지 않음을 나타내는 방식은 2가지가 있다

- undefined - 값을 할당하지 않았을 때 JS가 자동으로 할당해주는 값

  ```js
  let name
  
  console.log(name)
  ```

- null - 값이 없음을 나타내기 위해 사용한다

  ```js
  let name = null
  
  console.log(name)
  ```

  

```js
typeof null
"object"

typeof undefined
"undefined"
```



### 02.2 연산자

#### 할당 연산자

- 연산과 동시에 변수에 어떠한 값을 할당하는 연산자

```js
let c = 10

c += 10
console.log(c)

c -= 10
console.log(c)

c *= 10
console.log(c)

c /= 10
console.log(c)

c++  // 증강식 1을 더해주는 역할
console.log(c)  

c--  // 증감식 1을 빼주는 역할
console.log(c)  
```



#### 비교 연산자

- 두 값을 비교하기 위해 사용하며, `true` or `false` 를 반환한다.

```js
3 > 2 // true
3 < 2 // false
```

- 문자열도 비교가 가능하다. 영어 소문자가 대문자봐 큰 값을 가진다
- 알파벳은 오름차순으로 비교한다

```js
'A' < 'a'
```



#### 동등 연산자 (==)

- 형변환 했을 때 같은 값이면 일치한다고 본다.
- JS는 자동으로 형변환을 해준다
- 자동 형변환으로 인한 예기치 못한 상황이 발생할 수 있다. **그러므로 동등 연산자 사용은 지양한다.** 특수할 때는 사용할때도 있음

```js
const a = 1
const b = '1'

console.log(a == b)
>> true
console.log(a == number(b))
>> 와 같음
```



#### 일치 연산자 (===)

- 동등 연산자보다 엄격한 비교를 한다. **권장!!**

```javascript
const a = 1
const b = '1'

console.log(a === b)
>> false
console.log(a === number(b))
>> true
```



#### 논리 연산자

- `and` &&

  ```js
  true && true
  >> true
  
  true && false
  >> fales
  
  0 && 0 
  >> 0
  
  1 && 0
  >> 0
  
  4 && 7
  >> 7
  ```

  

- `or` ||

```js
true || false
>> true

false || true
>> true

1 || 0
>> 

4 || 7
>> 4
```



- `not` !

```js
!true
>> false
```



#### 삼항 연산자

- 가장 앞의 조건식이 참이면 `:` 을 기준으로 작성한 앞의 값이 반환되고, 반대의 경우 `:` 의 뒤의 값이 반환됨

```js
true ? 1 : 2s
>> 1
false ? 1 : 2
>> 2
```

```javascript
const redult = 3.14 > 4 ? 'Yes' : 'No'
console.log(result)
```





## 3. 조건문과 반복문

### 03.1 조건문

#### if, else if , else

- if

```javascript
const name = 'kim'

if (name === 'kim') {
    console.log('True')
}
```

- else if

```javascript
const name = 'kim'

if (name === 'lee') {
    console.log('LEE')
} else if (name === 'kim') {
    console.log('KIM')
}
```

- else

```javascript
const name = 'park'

if (name === 'lee') {
    console.log('LEE')
} else if (name === 'kim') {
    console.log('KIM')
} else {
    console.log(`${name}`)
}
```



#### switch

- 하나의 변수의 값에 따라 분기를 하는 조건문이다

```js
const name = '홍길동'

switch (name) {
    case 'admin': {
        console.log('ADMIN')
    }
    case 'manager': {
        console.log('MANAGER')
    }
    default: {
        console.log(`${name}`)
    }
}
```

- `case` 에 해당하는 값이 있다면, 그 내용을 실행하고, 그 다음도 실행하면서, default에 정의한 내용도 함께 실행된다.
- `break`와 함께 사용한다.

```js
const name = '홍길동'

switch (name) {
    case 'admin': {
        console.log('ADMIN')
        break
    }
    case 'manager': {
        console.log('MANAGER')
        break
    }
    default: {
        console.log(`${name}`)
    }
}
```



### 03.2 반복문

#### while

- `while` 키워드 뒤에 오는 조건이 `true` 인 동안 반복한다.

```js
let i = 0
while (i < 6) {
    console.log(i)
    i++
}

>> 
0
1
2
3
4
5
```



#### for

```js
for (let i = 0; i < 6; i++) {
    console.log(i)
}
```



#### for of

- 배열에서 <u>요소</u>를 하나씩 순회하며 반복하는 반복문.
- 블럭 내에서 변수로 선언되기 때문이다.

```js
const numbers = [1,2,3,4]

for (const number of numbers) {
    console.log(number)
}

>>
1
2
3
4
```



#### for in

- object의 key값을 순회하는 반복문.
- 배열의 경우 <u>index값</u>을 순회한다.

```js
const numbers = [1,2,3,4]

for (const number in numbers) {
    console.log(number)
}

>>
0
1
2
3

const fruits = {
    a: 'apple',
    b: 'banana'
}
for (const key in fruits) {
    console.log(key)
    console.log(fruits[key])
}

>>
a
apple
b
banana
```





## 4. Functions

### 04.1 functions

#### 선언식

```js
function add (num1, num2) {
    return num1 + num2
}

add(1, 3)

>> 4
```



#### 표현식

- 일반적으로 표현식은 익명 함수로 작성한다.
- 익명함수는 표현식에서만 사용 가능하다.

```js
const sub = function (num1, num2) {
    return num1 - num2
}

sub(3, 1)
```

```js
const mySub = function namedSub (num1, num2) {
    return num1 - num2
}

mySub(3, 1)
>> 2
namedSub(3, 1)
>> 오류<함수이름>
```

- 이런식으로 쓰면 오류에서 정확히 알 수 있다



#### 기본 인자

- `function (name = '홍길동')`  name = '' 스페이스 해주기

```js
const greeting = function (name = '홍길동') {
    return name
}
```



### 04.2 선언식 vs 표현식

```js
console.log(typeof add)
console.log(typeof sub)

>>
function
function
```



#### Hoisting

(나오면안좋다)

```js
add(2, 7)

function add (num1, num2) {
    return num1 + num2
}

>> 9
```

- 표현식은 함수를 변수에 할당했고, 일종의 변수처럼 작동한다.

```js
sub(1, 3)

const sub = function (num1, num2) {
    return num1 - num2
}

>> 오류
```

- var로 function 선언시

```js
var sub
sub(1, 3)

var sub = function (num1, num2) {
    return num1 - num2
}

>> 오류
```

- 그러므로 var안쓸것



### 04.3 Arrow Function

> function과 중괄호를 생량하여 코드를 줄이기 위해 고안된 단축 문법

1. function 생략 가능

2. 함수의 매개변수가 하나밖에 없다면 () 생략 가능

3. 함수의 바디 {} 안에 들어가는 표현식이 하나면 {} return 생략 가능

   

```javascript
const arrow = function (name) {
    return `${name}입니다`
}

// 1. function 생략
const arrow = (name) => {
    return `${name}입니다`
}

// 2. () 생략 가능
const arrow = name => {
    return `${name}입니다`
}

// 3. {}, return 생략 가능
const arrow = name => `${name}입니다`

arrow('홍길동')
```





## 5. Data Structure

### 05.1 Array

- 사용법

```js
const numbers = [1,2,3,4]

numbers[0]
>> 1
numbers[3]
>> 4
// number[-1] 안된다! >> undefined 출력
numbers.length
>> 4
```



#### 자주 사용하는 메서드

- `push` && `pop`

```js
numbers.push('5') // 5 새로운 배열의 길이

numbers.pop()  // '5' 가장 마지막 요소
```



- `reverse` 배열을 반대로 정렬

```js
numbers.reverse() // [4,3,2,1]
```



- `unshift` && `shift`

```javascript
numbers.unshift('a') // 5 새로운 배열의 길이
numbers // ['a', 1, 2, 3, 4]

numbers.shift() // 'a'가장 처음 요소
numbers
```



- `includes`

```js
numbers.includes(1)
>> true
numbers.includes(0)
>> false
```



- `indexOf`
- 배열에 특정 요소가 있는지 확인, 있으면 가장 첫번째로 찾은 요소의 그 index를 반환한다
- 없으면 -1을 반환한다

```js
numbers.indexOf(1)
>> 0
numbers.indexOf(0)
>> -1
```



- `join`

```js
numbers.join()
>> "1,2,3,4"

numbers.join('')
>> "1234"

numbers.join('-')
>> "1-2-3-4"
```



### 05.2 Object

- 사용법
- key값은 문자열 형태로 작성, value는 모든 형태가 작성될 수 있다.
- 한 단어가 아닐때 공백으로 띄어져있으면 반드시 문자열로 써주어야한다!

```js
const person = {
    name: '홍길동',
    'phone number': '010-1234-5678',
    pocket: {
        phone: 'galaxy note 9',
        earphone: 'buzz live',
        'note book': 'macbook'
    }
}
```



#### 요소 접근

- dot notation

```js
person.name  // '홍길동'
person['name']  // '홍길동'
person['phone number']  // '010-1234-5678' 얘는 필수로 []안에 넣어줘야함 ' '때문에
person.pocket  // object
person.pocket.phone  // 'galaxy note 9'
person.pocket['phone']  // 'galaxy note 9'
```



#### Object 축약 문법

- 객체를 정의할 때 key 값과 할당하는 변수의 이름이 같으면 축약이 가능하다

```js
const books = ['python', 'JS']

const professor = {
    ggu : ['django', 'JS'],
    json : ['python']
}

const anyThing = null

const hphk = {
    books,
    professor,
    anyThing,
}

console.log(hphk)
```



```js
const userInformation = {
    name: 'kim',
    userId: 'ggu'
}
```

- ES5 이전

```js
const name = userInformation.name
const userId = userInformation.userId

>> "kim"
>> "ggu"
```

- ES6+ 이후

```js
const { name } = userInformation
const { userId } = userInformation

>> "kim"
>> "ggu"
```



```js
function getUserInfo (userInformation) {
    console.log(`userName = ${userInformation.name}`)
}

getUserInfo(userInformation)

>> userName = kim

// 바뀐거
function getUserInfo ({name}) {
    console.log(`userName = ${name}`)
}
getUserInfo(userInformation)

>> userName = kim
```



### 05.3 JSON (JavaScript Object Notation)

- key -> value 처럼 생겼는데 실제로는 문자열
- Object처럼 쓰려면 Parsing 작업이 필요하다 



#### Object -> JSON(string)

```javascript
const jsonData = JSON.stringify({
    tea: '국화차',
    coffee: '아메리카노',
})

console.log(jsonData)  // {tea: '국화차', coffee: '아메리카노'}
console.log(typeof jsonData)  // string
```



#### JSON(string) -> Object(parsing)

```js
const parseData = JSON.parse(jsonData)

console.log(parseData)  // tea: '국화차', coffee: '아메리카노'}
console.log(typeof parseData)  // object
```



### 05.4 Array Helper Method

> helper 는 일종의 라이브러리
>
> ES5.1버전에 처음 등장. 본격적으로 사용된 것은 ES6 부터



#### forEach :star:

- 주어진 `callBack` 을 배열에 있는 각 요소를 오름차순으로 한번씩 실행한다.

```js
arr.forEach(callback(element, index, array))
```

- ex)

```js
const colors = ['red', 'blue', 'white']

colors.forEach(function (color) {
    console.log(color)
})

// 얘도 같음
colors.forEach(color => console.log(color))

>> 
red
blue
white
```

- `forEach`는 return 값이 없다

```js
const result = colors.forEach(color => console.log(color))
console.log(result)
```



#### map

- 배열의 모든 요소에 대해 `callback`을 실행한다. 함수의 반환값을 요소로 하는 새로운 배열을 반환
- 배열을 내가 원하는 다른 방식으로 바꿔야할 때 쓴다.

```js
arr.map(callback(element, index, array))
```

- ex)

```js
const numbers = [1,2,3]

const mapNumbers = numbers.map(function (number) {
    return number * 2
})

console.log(mapNumbers)

>> [2,4,6]
```



#### filter

- `callback` 함수를 실행했을 때, 어떠한 테스트 혹은 조건을 만족하고 통과하는 모든 요소를 모아서 새로운 배열을 반환한다.

```js
arr.filter(callback(element, index, array))
```

- ex)

```js
const products = [
    { name: 'cucumber', type: 'vegetable' },
    { name: 'banana', type: 'fruit' },
    { name: 'carrot', type: 'vegetable' },
    { name: 'apple', type: 'fruit' },
]

const fruits = products.filter(function (product) {
    return product.type === 'fruit'
})

console.log(fruits)
```



#### reduce

- 배열 내의 숫자 총합, 평균 계산 배열의 하나의 값으로 줄이는 동작

```js
arr.reduce(callback(acc, element, index, array), initialValue)
```

- 첫번째 매개변수 acc는 누적 값을 의미한다.

- 두번째 매개변수 initialValue는 초기값을 의미한다.

```js
const tests = [90, 90, 80, 77]

const sum = tests.reduce(function (total, x) {
    return total + x
}, 0)  // 여기서 0 생략 가능

console.log(sum)
```



#### find 

- callback을 만족하는 첫번째 요소를 찾아서 반환한다. 없으면 `undefined`를 반환한다. 

```js
arr.find(callback(element, index, array))
```

- ex)

```js
  const avengers = [
      { name: 'Tony Stark', age: 45 },
      { name: 'Steve Rogers', age: 32 },
      { name: 'Thor', age: 40 },
    ]

    const avenger = avengers.find(function (avenger) {
      return avenger.name === 'Tony Stark'
    })
console.log(avenger)
```



#### some

- 배열 안의 요소 중, 단 하나라도 조건을 만족한다면 true 반환, 아니면 false 반환

```js
arr.some(callback(element, index, array))
```

- ex)

```js
const arr = [1, 2, 3, 4, 5]

const result = arr.some(elem => elem % 2 === 0)  // true
console.log(result)
```



#### every

- 배열 안의 요소가 모두 조건을 만족해서 true 반환, 아니면 false 반환

```
arr.every(callback(element, index, array))
```

- ex)

```js
const arr = [1, 2, 3, 4, 5]

const result2 = arr.every(elem => elem % 2 === 0)  // false
console.log(result2)
```

