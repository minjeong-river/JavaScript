# 섹션 1. 자바스크립트의 기본문법

- 변수란?
- 자료형과 연산자
- 변수와 자료형 문제
- [보너스트랙: 호이스팅, let과 var의 차이](#보너스트랙-호이스팅-let과-var의-차이)
- [배열](#배열)
- 배열 문제
- 객체
- if문
- If문 문제
- 보너스 트랙: switch문과 삼항연산자
- 반복문
- 반복문 문제
- 보너스 트랙: 369문제 풀이해석
- 함수
- 함수 문제
- 보너스트랙: 함수문제4번 풀이
- 보너스트랙:함수5번문제풀이
- 보너스트랙:함수6번문제 풀이

---

## 보너스트랙: 호이스팅, let과 var의 차이

### 1. 호이스팅(Hoisting)
코드가 실행이 되기 전에 자바스크립트 엔진이 선언해둔 변수를 미리 조사하고,
선언된 변수랑 함수를 가져가서 메모리에 기억을 해둔다.
함수가 실행되기 전에 변수들을 범위의 최 상단으로 끌어올리는 것을 호이스팅이라고 한다. 

### 2. 호이스팅 시 발생되는 var의 문제점

호이스팅시 변수의 선언과 초기화(undefined으로)를 같이 시켜버린다.

```javascript
console.log(a); // undefined
var a = 1;
console.log(a); // 1 
```

```javascript
console.log(a); // undefined
a = 1;
var a;
console.log(a); // 1
```

함수만 지역변수로 호이스팅 되고 나머지(for, if 등)는 전역변수로 호이스팅 된다.

```javascript
 for(var i = 1; i<5; i++) {
    console.log(i); // 1 2 3 4
 }
 console.log(i);    // 1 2 3 4 5
```
변수 이름의 중복을 허용한다.

```javascript
var a = 1;
console.log(a); // 1
var a = 2;
console.log(a); // 2
```

### 3. let

let 키워드도 호이스팅 된다. let 키워드로 선언한 변수는 "선언 단계"와 "초기화 단계"가 분리되어 진행된다. 즉, 자바스크립트 엔진에 의해 암묵적으로 선언 단계가 먼저 실행되지만, 초기화 단계는 변수 선언문에 도달했을 때 실행된다. 따라서 초기화 단계가 실행되기 이전에 변수에 접근하려고 하면 참조 에러가 발생한다.  

let 키워드로 선언한 변수는 스코프의 시작 시점부터 초기화 단계 시작 지점(변수 선언문)까지 변수를 참조할 수 없다. 스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 일시적 사각지대 **TDZ(Temporal Dead Zone)** 이라고 부른다.

```javascript
console.log(a); // Cannot access 'a' before initialization error
let a = 1;
console.log(a); // 1 
```

블록 레벨 스코프 : 블록 내에 선언된 변수(지역변수)는 스코프를 벗어나면 사용할 수 없다.

```javascript
 for(let i = 1; i<5; i++) {
    console.log(i); // 1 2 3 4
 }
 console.log(i);    // i is not defined error
```

변수 중복 선언 금지

```javascript
let a = 1;
console.log(a);
let a = 2;
console.log(a);

//  identifier 'a' has already been declared error
```

---

## 배열

```javascript
let fruit = ['banana', 'apple', 'grape', 'mango'];

console.log(fruit)      // ['banana', 'apple', 'grape', 'mango']
console.log(fruit[3])   // mango
```

### 1. 배열 값 변경

```javascript
fruitp[0] = 'cherry';
fruit[3] = 'tomato';
console.log(frult);     // ['cherry', 'apple', 'tomato', mango]
```

### 2. pop() : 마지막에 있는 아이템 제거

```javascript
fruit.pop();
console.log(fruit);     // mango
```

### 3. push() : 마지막 인덱스 위치에 아이템 추가

```javascript
fruit.push('pineapple');
console.log(frult);     // pineapple
```

### 4. includes() : 해당 아이템을 배열이 포함하고 있는지 알려줌

```javascript
console.log(fruit.includes('apple'));  // true
```

### 5. indexOf() : 인덱스 번호 확인

```javascript
console.log(fruit.indexOf('apple'));   // 1
```

### 6. slice() : 배열 아이템을 잘라내는 역할 (시작점, 끝점-끝점 미포함)

slice()는 기존의 배열을 건드리지 않는다. slice() 후 새로운 배열을 만든다.

```javascript
console.log(fruit.slice(1));     // ['apple', 'tomato', 'pineapple']
console.log(fruit.slice(1,3));   // ['apple', 'tomato'];

fruit.slice(1,3);                // ['apple', 'tomato'];
console.log(fruit);              // ['cherry', 'apple', 'tomato', mango]
```

### 7. splice : 시작점으로부터 몇 개의 아이템을 제거하고 싶은지

splice()는 기존의 배열이 잘린다.

```javascript
fruit.splice(2,1);
console.log(fruit);  // ['cherry', 'apple', 'pineapple']
```

---

## 객체

```javascript
let patient = {
   name : "jimin",
   age : 17,
   disease : "cold"
}

console.log(patient);         // {name: 'jimin', age: 17, disease: 'cold'}
console.log(patient.name);    // jimin
console.log(patient["name"])  // jimin
```

### 1. 값 변경

```javascript
patient.name = "jk";
patient["age"] = 25;
console.log(patient);   // {name: 'jk', age: 25, disease: 'cold'}
```

### 2. 객체를 배열에 넣기

```javascript
let patientList = [
   {name:"jimin", age: 13},
   {name:"jk", age:25},
   {name:"jhope", age:40}
];

console.log(patientList);  // {name: 'jimin', age: 13}
                           // {name: 'jk', age: 25}
                           // {name: 'jhope', age: 40}
```

### 3. 배열 안에 있는 객체 값 출력

```javascript
console.log(patientList[0].name);   // jimin
console.log(patientList[1].name);   // jk
console.log(patientList[1].name);   // jhope
```