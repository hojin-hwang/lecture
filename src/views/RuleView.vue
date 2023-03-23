<template>
  <section>
    <nav class="subject">
        <ul>
          <li><a href="#variables">변수</a></li>
          <li><a href="#function">함수</a>
              <ul>
                  <li><a href="#function_1">기본 메개변수값을 주는게 좋다</a></li>
                  <li><a href="#function_2">함수 인자는 2개 이하가 이상적</a></li>
                  <li><a href="#function_3">함수는 하나의 행동만</a></li>
                  <li><a href="#function_4">중복된 코드</a></li>
                  <li><a href="#function_5">기본객체는 Object.assign을 사용</a></li>
                  <li><a href="#function_6">😾 매개변수로 플래그</a></li>
                  <li><a href="#function_7">😾 전역 함수</a></li>
                  <li><a href="#function_8">사이트 이펙트 피하기 #1</a></li>
                  <li><a href="#function_9">사이트 이펙트 피하기 #2</a></li>
                  <li><a href="#function_10"> 함수형 프로그래밍</a></li>
                  <li><a href="#function_11">조건문의 캡슐화</a></li>
                  <li><a href="#function_12">조건문을 피해라</a></li>
                  <li><a href="#function_13">타입-체킹 피하기 #1</a></li>
                  <li><a href="#function_14">타입-체킹 피하기 #2</a></li>
                  <li><a href="#function_15">과도한 최적화를 지양</a></li>
              </ul>
          </li>
          <li><a href="#object">객체와 자료구조</a>
              <ul>
                  <li><a href="#object_1">Use getter & setter</a></li>
                  <li><a href="#object_2">객체에 비공개 멤버 만들기</a></li>
              </ul>
          </li>
          <li><a href="#class">클래스</a>
              <ul>
                  <li><a href="#class_1">ES5의 함수 -> ES6의 클래스</a></li>
                  <li><a href="#class_2">메소드 체이닝</a></li>
              </ul>
          </li>
          <li><a href="#etc">ETC</a>
              <ul>
                  <li><a href="#etc_1">단일 책임 원칙 (Single Responsibility Principle, SRP)</a></li>
                  <li><a href="#etc_2">개방/폐쇄 원칙</a></li>
                  <li><a href="#etc_3">리스코프 치환 원칙</a></li>
                  <li><a href="#etc_4">인터페이스 분리 원칙</a></li>
                  <li><a href="#etc_5">의존성 역전 원칙</a></li>
              </ul>
          </li>
          <li><a href="#test">테스트</a></li>
          <li><a href="#concurrency">동시성</a>
              <ul>
                  <li><a href="#concurrency_1">Callback 대신 Promise를 사용</a></li>
                  <li><a href="#concurrency_2">Async/Await은 Promise보다 더욱 깔끔</a></li>
              </ul>
          </li>
          <li><a href="#error">에러 처리</a>
              <ul>
                  <li><a href="#error_1">단순히 에러를 확인만 하지마세요</a></li>
                  <li><a href="#error_2">Promise가 실패된 것을 무시하지 마세요</a></li>
              </ul>
          </li>
      </ul>
    </nav>
    <main>

      <h3  id="variables">변수</h3>
<article class="info">
변수이름에 중복을 피하자 : Car.carModel -> Car.mode;
</article>    
    <pre v-highlightjs>
        <code class="hljs javascript">
const Car = {
    carMake: 'BMW',
    carModel: 'M3',
    carColor: '파란색'
};

const Car = {
    make: 'BMW',
    model: 'M3',
    color: '파란색'
};
</code></pre>
<!---------------------------->

<hr>
<h3 id="function">함수(Functions)</h3>
<article class="info"  id="function_1">
   기본 메개변수값을 주는게 좋다
</article>    
    <pre v-highlightjs>
        <code class="hljs javascript">
function createMicrobrewery(name) {
    const breweryName = name || 'Hipster Brew Co.';
    // ...
    }

function createMicrobrewery(name = 'Hipster Brew Co.') {
  // ... Null Check할 필요 없음
}
</code></pre>
<!---------------------------->
<article class="info" id="function_2">
    함수 인자는 2개 이하가 이상적입니다
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">
function createMenu(title, body, buttonText, cancellable) {
    // ...
}
 
function createMenu({ title, body, buttonText, cancellable }) {
// ...
}

createMenu({title: 'Foo',body: 'Bar',buttonText: 'Baz',cancellable: true});
 </code></pre>
 <!---------------------------->
    
 <article class="info"  id="function_3">
    함수는 하나의 행동만 해야합니다. ***** 
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">
function emailClients(clients) {
    clients.forEach(client => {
        const clientRecord = database.lookup(client);
        if (clientRecord.isActive()) {
        email(client);
        }
    });
}

function emailClients(clients) {
    clients
      .filter(isClientActive)
      .forEach(email);
}
  
function isClientActive(client) {
    const clientRecord = database.lookup(client);
    return clientRecord.isActive();
}
 </code></pre>
 <!---------------------------->

 <article class="info"  id="function_4">
    중복된 코드를 피하자 ***
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
function showDeveloperList(developers) {
    developers.forEach(developers => {
        const expectedSalary = developer.calculateExpectedSalary();
        const experience = developer.getExperience();
        const githubLink = developer.getGithubLink();
        const data = {
        expectedSalary,
        experience,
        githubLink
        };
    
        render(data);
    });
    }
    
function showManagerList(managers) {
    managers.forEach(manager => {
        const expectedSalary = manager.calculateExpectedSalary();
        const experience = manager.getExperience();
        const portfolio = manager.getMBAProjects();
        const data = {
        expectedSalary,
        experience,
        portfolio
        };

        render(data);
    });
}
//Good
function showEmployeeList(employees) {
    employees.forEach((employee) => {
      const expectedSalary = employee.calculateExpectedSalary();
      const experience = employee.getExperience();
  
      let portfolio = employee.getGithubLink();
  
      if (employee.type === 'manager') {
        portfolio = employee.getMBAProjects();
      }
  
      const data = {
        expectedSalary,
        experience,
        portfolio
      };
  
      render(data);
    });
}
 </code></pre>
 <!---------------------------->

 <article class="info"  id="function_5">
    기본객체는 Object.assign을 사용 **
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
const menuConfig = {
    title: null,
    body: 'Bar',
    buttonText: null,
    cancellable: true
    };
    
function createMenu(config) 
{
    config.title = config.title || 'Foo';
    config.body = config.body || 'Bar';
    config.buttonText = config.buttonText || 'Baz';
    config.cancellable = config.cancellable !== undefined ? config.cancellable : true;
}
    
createMenu(menuConfig);

//Good
const menuConfig = {
    title: 'Order',
    // 유저가 'body' key의 value를 정하지 않았다.
    buttonText: 'Send',
    cancellable: true
  };
  
function createMenu(config) 
{
    config = Object.assign({
        title: 'Foo',
        body: 'Bar',
        buttonText: 'Baz',
        cancellable: true
    }, config);

    // config는 이제 다음과 동일합니다: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
    // ...
}

createMenu(menuConfig);
 </code></pre>
 <!---------------------------->

 <article class="info"  id="function_6">
    매개변수로 플래그를 사용하지 마세요. boolean 기반으로 함수가 실행되는 코드가 나뉜다면 함수를 분리하세요.
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
function createFile(name, temp) {
    if (temp) {
        fs.create(`./temp/${name}`);
    } else {
        fs.create(name);
    }
}

//Good
function createFile(name) {
    fs.create(name);
}
  
function createTempFile(name) {
    createFile(`./temp/${name}`);
}
 </code></pre>
 <!---------------------------->

 <article class="info"  id="function_7">
    전역 함수를 사용하지 마세요
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
// 아래 함수에 의해 참조되는 전역 변수입니다.
// 이 전역 변수를 사용하는 또 하나의 함수가 있다고 생각해보세요. 이제 이 변수는 배열이 될 것이고, 프로그램을 망가뜨리겠죠.
let name = 'Ryan McDermott';

function splitIntoFirstAndLastName() {
    name = name.split(' ');
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];

//Good
function splitIntoFirstAndLastName(name) {
    return name.split(' ');
}
  
const name = 'Ryan McDermott';
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
 </code></pre>
 <!---------------------------->

 <article class="info"  id="function_8">
    사이트 이펙트 피하기 #1
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
const addItemToCart = (cart, item) => {
    cart.push({ item, date: Date.now() });
    };

//Good
const addItemToCart = (cart, item) => {
    return [...cart, { item, date : Date.now() }];
}
 </code></pre>
 <!---------------------------->


 <article class="info"  id="function_9">
    사이트 이펙트 피하기 #2
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
// 아래 함수에 의해 참조되는 전역 변수입니다.
// 이 전역 변수를 사용하는 또 하나의 함수가 있다고 생각해보세요. 이제 이 변수는 배열이 될 것이고, 프로그램을 망가뜨리겠죠.
let name = 'Ryan McDermott';

function splitIntoFirstAndLastName() {
    name = name.split(' ');
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];

//Good
function splitIntoFirstAndLastName(name) {
    return name.split(' ');
}
  
const name = 'Ryan McDermott';
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
 </code></pre>
 <!---------------------------->

 <article class="info"  id="function_10">
    명령형 프로그래밍보다 함수형 프로그래밍을 지향
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
const programmerOutput = [
{
    name: 'Uncle Bobby',
    linesOfCode: 500
}, {
    name: 'Suzie Q',
    linesOfCode: 1500
}, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
}, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
}];

let totalOutput = 0;

for (let i = 0; i &lt; programmerOutput.length; i++) {
totalOutput += programmerOutput[i].linesOfCode;
}

//Good
const totalOutput = programmerOutput
  .map(programmer => programmer.linesOfCode)
  .reduce((acc, linesOfCode) => acc + linesOfCode, INITIAL_VALUE)
 </code></pre>
 <!---------------------------->

 <article class="info"  id="function_11">
    조건문의 캡슐화!
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
if (fsm.state === 'fetching' && isEmpty(listNode)) {
    // ...
    }

//Good
function shouldShowSpinner(fsm, listNode) {
    return fsm.state === 'fetching' && isEmpty(listNode);
}
  
if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
// ...
}
 </code></pre>
 <!---------------------------->

 <article class="info"  id="function_12">
    조건문 작성을 피해보자
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
class Airplane {
    // ...
    getCruisingAltitude() {
        switch (this.type) {
        case '777':
            return this.getMaxAltitude() - this.getPassengerCount();
        case 'Air Force One':
            return this.getMaxAltitude();
        case 'Cessna':
            return this.getMaxAltitude() - this.getFuelExpenditure();
        }
    }
    }

//Good
class Airplane {
    // ...
}

class Boeing777 extends Airplane {
    // ...
    getCruisingAltitude() {
        return this.getMaxAltitude() - this.getPassengerCount();
    }
}

class AirForceOne extends Airplane {
    // ...
    getCruisingAltitude() {
        return this.getMaxAltitude();
    }
}

class Cessna extends Airplane {
    // ...
    getCruisingAltitude() {
        return this.getMaxAltitude() - this.getFuelExpenditure();
    }
}
 </code></pre>
 <!---------------------------->
 <article class="info"  id="function_13">
    타입-체킹 피하기 #1
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//첫번째 방법은 일관성 있는 API를 사용하는 것입니다.
//Bad            
function travelToTexas(vehicle) {
    if (vehicle instanceof Bicycle) {
        vehicle.pedal(this.currentLocation, new Location('texas'));
    } else if (vehicle instanceof Car) {
        vehicle.drive(this.currentLocation, new Location('texas'));
    }
}

//Good
function travelToTexas(vehicle) {
    vehicle.move(this.currentLocation, new Location('texas'));
}
 </code></pre>
 <!---------------------------->

 <article class="info"  id="function_14">
    타입-체킹 피하기 #2
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//TypeScript를 사용하는 것입니다. 
//JavaScript로 코드를 작성할땐 깔끔하게 코드를 작성하고, 좋은 테스트 코드를 짜야하며 좋은 코드 리뷰를 해야합니다
//Bad
function combine(val1, val2) {
    if (typeof val1 === 'number' && typeof val2 === 'number' ||
        typeof val1 === 'string' && typeof val2 === 'string') {
        return val1 + val2;
    }
    throw new Error('Must be of type String or Number');
}

//Good
function combine(val1, val2) {
    return val1 + val2;
}
 </code></pre>
 <!---------------------------->
 <article class="info"  id="function_15">
    과도한 최적화를 지양
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad            
// 오래된 브라우저의 경우 캐시되지 않은 `list.length`를 통한 반복문은 높은 코스트를 가졌습니다.
// 그 이유는 `list.length`를 매번 계산해야만 했기 때문인데, 최신 브라우저에서는 이것이 최적화 되었습니다.
for (let i = 0, len = list.length; i &lt; len; i++) {
    // ...
}

//Good
for (let i = 0; i &lt; list.length; i++) {
    // ...
}
 </code></pre>
 <!---------------------------->

<hr>
<h3  id="object">객체와 자료구조(Objects and Data Structures)</h3>
<article class="info"  id="object_1">
    Use getter & setter
    <ul>
        <li>객체의 속성을 얻는 것 이상의 많은 것을 하고싶을 때, 코드에서 모든 접근자를 찾아 바꾸고 할 필요가 없습니다.</li>
        <li>set할때 검증로직을 추가하는 것이 코드를 더 간단하게 만듭니다.</li>
        <li>내부용 API를 캡슐화 할 수 있습니다.</li>
        <li>getting과 setting할 때 로그를 찾거나 에러처리를 하기 쉽습니다.</li>
        <li>서버에서 객체 속성을 받아올 때 lazy load 할 수 있습니다.</li>
    </ul>
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad            
function makeBankAccount() {
    // ...
    
    return {
        // ...
        balance: 0
    };
 }
    
const account = makeBankAccount();
account.balance = 100;

//Good
function makeBankAccount() {
// private으로 선언된 변수
    let balance = 0;

    // 아래 return을 통해 public으로 선언된 "getter"
    function getBalance() {
        return balance;
    }

    // 아래 return을 통해 public으로 선언된 "setter"
    function setBalance(amount) {
        // ... balance를 업데이트하기 전 검증로직
        balance = amount;
    }

    return {
        // ...
        getBalance,
        setBalance
    };
}

const account = makeBankAccount();
account.setBalance(100);
//////////////////////////////////////
class BankAccount
{
// private으로 선언된 변수
  construct()
  {
  	this.balance = 0;

  }
    // 아래 return을 통해 public으로 선언된 "getter"
    getBalance() {
        return this.balance;
    }

    // 아래 return을 통해 public으로 선언된 "setter"
    setBalance(amount) {
        // ... balance를 업데이트하기 전 검증로직
        this.balance = amount;
    }
}

const account = new BankAccount();
account.setBalance(100);
 </code></pre>
 <!---------------------------->
 <article class="info"  id="object_2">
    객체에 비공개 멤버 만들기
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad            
const Employee = function(name) {
    this.name = name;
};
    
Employee.prototype.getName = function getName() {
    return this.name;
};
    
const employee = new Employee('John Doe');
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: undefined

//Good
function makeEmployee(name) {
    return {
        getName() {
        return name;
        },
    };
}

const employee = makeEmployee('John Doe');
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
 </code></pre>
 <!---------------------------->
 <hr>
<h3  id="class">클래스(Classes)</h3>
<article class="info"  id="class_1">
    ES5의 함수 -> ES6의 클래스
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//*크고 더 복잡한 객체가 필요한 경우가 아니라면 클래스보다 작은 함수를 사용
//Bad            
const Animal = function(age) {
    if (!(this instanceof Animal)) {
        throw new Error("Instantiate Animal with `new`");
    }
    this.age = age;
};
  
Animal.prototype.move = function() {};

const Mammal = function(age, furColor) {
    if (!(this instanceof Mammal)) {
        throw new Error("Instantiate Mammal with `new`");
}

Animal.call(this, age);
    this.furColor = furColor;
};
  
Mammal.prototype = Object.create(Animal.prototype);
Mammal.prototype.constructor = Mammal;
Mammal.prototype.liveBirth = function liveBirth() {};

const Human = function(age, furColor, languageSpoken) {
    if (!(this instanceof Human)) {
    throw new Error("Instantiate Human with `new`");
}

Mammal.call(this, age, furColor);
    this.languageSpoken = languageSpoken;
};
  
Human.prototype = Object.create(Mammal.prototype);
Human.prototype.constructor = Human;
Human.prototype.speak = function speak() {};

//Good
class Animal {
    constructor(age) {
    this.age = age;
}

move() { /* ... */ }
}

class Mammal extends Animal {
constructor(age, furColor) {
    super(age);
    this.furColor = furColor;
}

liveBirth() { /* ... */ }
}

class Human extends Mammal {
constructor(age, furColor, languageSpoken) {
    super(age, furColor);
    this.languageSpoken = languageSpoken;
}

speak() { /* ... */ }
}
 </code></pre>
 <!---------------------------->

 <article class="info" id="class_2">
    메소드 체이닝
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">
class Car 
{
    constructor() {
        this.make = 'Honda';
        this.model = 'Accord';
        this.color = 'white';
    }
    
    setMake(make) {
        this.make = make;
        // 메모: 체이닝을 위해 this를 리턴합니다.
        return this;
    }
    
    setModel(model) {
        this.model = model;
        // 메모: 체이닝을 위해 this를 리턴합니다.
        return this;
    }
    
    setColor(color) {
        this.color = color;
        // 메모: 체이닝을 위해 this를 리턴합니다.
        return this;
    }
    
    save() {
        console.log(this.make, this.model, this.color);
        // 메모: 체이닝을 위해 this를 리턴합니다.
        return this;
    }
}
    
const car = new Car()
.setColor('pink')
.setMake('Ford')
.setModel('F-150')
.save();
 </code></pre>
 <!---------------------------->

 <article class="info"  id="class_3">
    상속보단 조합(composition)
    <ul>
        <li>당신의 상속관계가 "has-a" 관계가 아니라 "is-a" 관계일 때 (사람->동물 vs. 유저->유저정보)</li>
        <li>기반 클래스의 코드를 다시 사용할 수 있을 때 (인간은 모든 동물처럼 움직일 수 있습니다.).</li>
        <li>기반 클래스를 수정하여 파생된 클래스 모두를 수정하고 싶을 때 (이동시 모든 동물이 소비하는 칼로리를 변경하고 싶을 때)</li>
    </ul>
 </article>    
<pre v-highlightjs>
    <code class="hljs javascript">//Bad            
class Employee {
    constructor(name, email) {
        this.name = name;
        this.email = email;
    }
    
    // ...
 }
    
// 이 코드가 안좋은 이유는 Employees가 tax data를 "가지고" 있기 때문입니다.
// EmployeeTaxData는 Employee 타입이 아닙니다.
class EmployeeTaxData extends Employee {
    constructor(ssn, salary) {
        super();
        this.ssn = ssn;
        this.salary = salary;
    }

// ...
}

//Good
class EmployeeTaxData {
    constructor(ssn, salary) {
        this.ssn = ssn;
        this.salary = salary;
    }

// ...
}
  
class Employee {
    constructor(name, email) {
        this.name = name;
        this.email = email;
    }

    setTaxData(ssn, salary) {
        this.taxData = new EmployeeTaxData(ssn, salary);
    }
    // ...
}
 </code></pre>
 <!---------------------------->

 <hr>
 <h3  id="etc">ETC</h3>
 <article class="info"  id="etc_1">
    단일 책임 원칙 (Single Responsibility Principle, SRP)
    - 하나의 클래스에 너무 많은 기능을 넣지 말자.
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
class UserSettings {
    constructor(user) {
        this.user = user;
    }
    
    changeSettings(settings) {
        if (this.verifyCredentials()) {
        // ...
        }
    }
    
    verifyCredentials() {
        // ...
    }
}

//Good
class UserAuth {
    constructor(user) {
      this.user = user;
    }
  
    verifyCredentials() {
      // ...
    }
}
    
class UserSettings {
    constructor(user) {
        this.user = user;
        this.auth = new UserAuth(user);
    }
  
    changeSettings(settings) {
      if (this.auth.verifyCredentials()) {
        // ...
      }
    }
}
 </code></pre>
 <!---------------------------->

 <article class="info"  id="etc_2">
    개방/폐쇄 원칙 (Open/Closed Principle, OCP
    - 사용자가 .js 소스 코드 파일을 열어 수동으로 조작하지 않고도 모듈의 기능을 확장하도록 허용해야한다
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
class AjaxAdapter extends Adapter {
    constructor() {
        super();
        this.name = 'ajaxAdapter';
    }
}
    
class NodeAdapter extends Adapter {
    constructor() {
        super();
        this.name = 'nodeAdapter';
    }
}
    
class HttpRequester {
    constructor(adapter) {
        this.adapter = adapter;
    }
    
    fetch(url) {
        if (this.adapter.name === 'ajaxAdapter') {
            return makeAjaxCall(url).then((response) => {
                // transform response and return
            });
        } 
        else if (this.adapter.name === 'httpNodeAdapter') {
            return makeHttpCall(url).then((response) => {
                // transform response and return
            });
        }
    }
}
    
function makeAjaxCall(url) {
    // request and return promise
}

function makeHttpCall(url) {
    // request and return promise
}

//Good
class AjaxAdapter extends Adapter {
    constructor() {
      super();
      this.name = 'ajaxAdapter';
    }
  
    request(url) {
      // request and return promise
    }
}
  
class NodeAdapter extends Adapter {
    constructor() {
        super();
        this.name = 'nodeAdapter';
    }

    request(url) {
        // request and return promise
    }
}
  
class HttpRequester {
    constructor(adapter) {
        this.adapter = adapter;
    }

    fetch(url) {
        return this.adapter.request(url).then((response) => {
        // transform response and return
        });
    }
}
 </code></pre>
 <!---------------------------->

 <article class="info"  id="etc_3">
    리스코프 치환 원칙 (Liskov Substitution Principle, LSP)
    <p>
        수학적으로 정사각형은 직사각형이지만 상속을 통해 "is-a" 관계를 사용하여 모델링한다면 문제가 발생합니다.
    </p>
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
class Rectangle {
    constructor() {
        this.width = 0;
        this.height = 0;
    }
    
    setColor(color) {
        // ...
    }
    
    render(area) {
        // ...
    }
    
    setWidth(width) {
        this.width = width;
    }
    
    setHeight(height) {
        this.height = height;
    }
    
    getArea() {
        return this.width * this.height;
    }
}
    
class Square extends Rectangle {
    setWidth(width) {
        this.width = width;
        this.height = width;
    }
    
    setHeight(height) {
        this.width = height;
        this.height = height;
    }
}
    
function renderLargeRectangles(rectangles) {
    rectangles.forEach((rectangle) => {
        rectangle.setWidth(4);
        rectangle.setHeight(5);
        const area = rectangle.getArea(); // 정사각형일때 25를 리턴합니다. 하지만 20이어야 하는게 맞습니다.
        rectangle.render(area);
    });
}
    
const rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles(rectangles);

//Good
class Shape {
    setColor(color) {
        // ...
    }

    render(area) {
        // ...
    }
}
  
class Rectangle extends Shape {
    constructor(width, height) {
      super();
      this.width = width;
      this.height = height;
    }
  
    getArea() {
      return this.width * this.height;
    }
}
  
class Square extends Shape {
    constructor(length) {
      super();
      this.length = length;
    }
  
    getArea() {
      return this.length * this.length;
    }
}
  
function renderLargeShapes(shapes) {
    shapes.forEach((shape) => {
        const area = shape.getArea();
        shape.render(area);
      });
}
  
const shapes = [new Rectangle(4, 5), new Rectangle(4, 5), new Square(5)];
renderLargeShapes(shapes);
 </code></pre>
 <!---------------------------->

 <article class="info" id="etc_4">
    인터페이스 분리 원칙 (Interface Segregation Principle, ISP)
    <p>
        무거운 인터페이스(fat interface)"를 만드는 것을 방지
    </p>
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
class DOMTraverser {
    constructor(settings) {
        this.settings = settings;
        this.setup();
    }
    
    setup() {
        this.rootNode = this.settings.rootNode;
        this.animationModule.setup();
    }
    
    traverse() {
        // ...
    }
}
    
const $ = new DOMTraverser({
    rootNode: document.getElementsByTagName('body'),
    animationModule() {} // 우리는 대부분의 경우 DOM을 탐색할 때 애니메이션이 필요하지 않습니다.
    // ...
});

//Good
class DOMTraverser {
    constructor(settings) {
      this.settings = settings;
      this.options = settings.options;
      this.setup();
    }
  
    setup() {
      this.rootNode = this.settings.rootNode;
      this.setupOptions();
    }
  
    setupOptions() {
      if (this.options.animationModule) {
        // ...
      }
    }
  
    traverse() {
      // ...
    }
}
  
const $ = new DOMTraverser({
    rootNode: document.getElementsByTagName('body'),
    options: {
      animationModule() {}
    }
});
 </code></pre>
 <!---------------------------->

 <article class="info" id="etc_5">
    의존성 역전 원칙 (Dependency Inversion Principle, DIP)
    <ul>
        <li>상위 모듈은 하위 모듈에 종속되어서는 안됩니다. 둘 다 추상화에 의존해야 합니다.</li>
        <li>추상화는 세부사항에 의존하지 않습니다. 세부사항은 추상화에 의해 달라져야 합니다.</li>
    </ul>
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
class InventoryRequester {
    constructor() {
        this.REQ_METHODS = ['HTTP'];
    }
    
    requestItem(item) {
        // ...
    }
}
    
class InventoryTracker {
    constructor(items) {
        this.items = items;
    
        // 안좋은 이유: 특정 요청방법 구현에 대한 의존성을 만들었습니다.
        // requestItems는 한가지 요청방법을 필요로 합니다.
        this.requester = new InventoryRequester();
    }
    
    requestItems() {
        this.items.forEach(item => {
        this.requester.requestItem(item);
        });
    }
}
    
const inventoryTracker = new InventoryTracker(['apples', 'bananas']);
inventoryTracker.requestItems();

//Good
class InventoryTracker {
    constructor(items, requester) {
      this.items = items;
      this.requester = requester;
    }
  
    requestItems() {
      this.items.forEach(item => {
        this.requester.requestItem(item);
      });
    }
}
  
class InventoryRequesterV1 {
    constructor() {
        this.REQ_METHODS = ['HTTP'];
    }

    requestItem(item) {
        // ...
    }
}

class InventoryRequesterV2 {
    constructor() {
        this.REQ_METHODS = ['WS'];
    }

    requestItem(item) {
        // ...
    }
}
  
// 의존성을 외부에서 만들어 주입해줌으로써,
// 요청 모듈을 새롭게 만든 웹소켓 사용 모듈로 쉽게 바꿔 끼울 수 있게 되었습니다.
const inventoryTracker = new InventoryTracker(['apples', 'bananas'], new InventoryRequesterV2());
inventoryTracker.requestItems();
 </code></pre>
 <!---------------------------->

 <hr>
 <h3 id="test">테스트(Testing)</h3>
 <article class="info"  id="test_1">
    테스트 컨셉
   -테스트 주도 개발 방법론(Test Driven Development, TDD)도 좋다!
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
const assert = require('assert');

describe('MakeMomentJSGreatAgain', () => {
    it('handles date boundaries', () => {
    let date;

    date = new MakeMomentJSGreatAgain('1/1/2015');
    date.addDays(30);
    assert.equal('1/31/2015', date);

    date = new MakeMomentJSGreatAgain('2/1/2016');
    date.addDays(28);
    assert.equal('02/29/2016', date);

    date = new MakeMomentJSGreatAgain('2/1/2015');
    date.addDays(28);
    assert.equal('03/01/2015', date);
    });
});

//Good
const assert = require('assert');

describe('MakeMomentJSGreatAgain', () => {
  it('handles 30-day months', () => {
    const date = new MakeMomentJSGreatAgain('1/1/2015');
    date.addDays(30);
    assert.equal('1/31/2015', date);
  });

  it('handles leap year', () => {
    const date = new MakeMomentJSGreatAgain('2/1/2016');
    date.addDays(28);
    assert.equal('02/29/2016', date);
  });

  it('handles non-leap year', () => {
    const date = new MakeMomentJSGreatAgain('2/1/2015');
    date.addDays(28);
    assert.equal('03/01/2015', date);
  });
});
 </code></pre>
 <!---------------------------->

 <hr>
 <h3 id="Concurrency">동시성(Concurrency)</h3>
 <article class="info" id="concurrency_1">
    Callback 대신 Promise를 사용
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
require('request').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', (requestErr, response) => {
    if (requestErr) {
        console.error(requestErr);
    } else {
        require('fs').writeFile('article.html', response.body, (writeErr) => {
        if (writeErr) {
            console.error(writeErr);
        } else {
            console.log('File written');
        }
        });
    }
});

//Good
require('request-promise').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
  .then((response) => {
    return require('fs-promise').writeFile('article.html', response);
  })
  .then(() => {
    console.log('File written');
  })
  .catch((err) => {
    console.error(err);
  });
});
 </code></pre>
 <!---------------------------->

 <article class="info" id="concurrency_2">
    Async/Await은 Promise보다 더욱 깔끔
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
require('request-promise').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
.then(response => {
    return require('fs-promise').writeFile('article.html', response);
})
.then(() => {
    console.log('File written');
})
.catch(err => {
    console.error(err);
})

//Good
async function getCleanCodeArticle() {
    try {
      const response = await require('request-promise').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin');
      await require('fs-promise').writeFile('article.html', response);
      console.log('File written');
    } catch(err) {
      console.error(err);
    }
  }
 </code></pre>
 <!---------------------------->

 <hr>
 <h3  id="error">에러 처리(Error Handling)</h3>
 <article class="info"  id="error_1">
    단순히 에러를 확인만 하지마세요
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
try {
    functionThatMightThrow();
    } catch (error) {
    console.log(error);
}

//Good
try {
    functionThatMightThrow();
} 
catch (error) {
    // 첫번째 방법은 console.error를 이용하는 것입니다. 이건 console.log보다 조금 더 알아채기 쉽습니다.
    console.error(error);
    // 다른 방법은 유저에게 알리는 방법입니다.
    notifyUserOfError(error);
    // 또 다른 방법은 서비스 자체에 에러를 기록하는 방법입니다.
    reportErrorToService(error);
    // 혹은 그 어떤 방법이 될 수 있습니다.
}
 </code></pre>
 <!---------------------------->

 <article class="info"  id="error_2">
    Promise가 실패된 것을 무시하지 마세요
 </article>    
     <pre v-highlightjs>
         <code class="hljs javascript">//Bad
getdata()
.then(data => {
    functionThatMightThrow(data);
})
.catch(error => {
    console.log(error);
});

//Good
getdata()
.then(data => {
  functionThatMightThrow(data);
})
.catch(error => {
  // 첫번째 방법은 console.error를 이용하는 것입니다. 이건 console.log보다 조금 더 알아채기 쉽습니다.
  console.error(error);
  // 다른 방법은 유저에게 알리는 방법입니다.
  notifyUserOfError(error);
  // 또 다른 방법은 서비스 자체에 에러를 기록하는 방법입니다.
  reportErrorToService(error);
  // 혹은 그 어떤 방법이 될 수 있습니다.
});
 </code></pre>

    </main>
  </section>
</template>

<style scoped>
main{
  padding: 0 1rem;
}
@media (min-width: 1024px) {
  section {
    min-height: 100vh;
    display: flex;
    align-items: flex-start;
    padding: 1rem 0;
  }
}
</style>
