<template>
  <section>
    <nav class="subject">
        <ul>
            <li><a href="#callback">Callback</a></li>
            <li><a href="#promise">Promise</a></li>
            <li><a href="#async">Async & Await</a></li>
            <li><a href="#filter">Filter</a></li>
            <li><a href="#private">Private</a></li>
            <li><a href="#assert">Assert</a></li>
            <li><a href="#ajax">RequestURL(without jQuery)</a></li>
        </ul>
    </nav>
    <main>

      <article class="code">
        <h3 id="callback">Callback Function</h3>
        <pre v-highlightjs><code class="hljs javascript">const callbackFunction = (agr_1 = null, arg_2 = {}, callback) =>
{
    const args = {};
    args.arg_1 = arg_1;
    args.arg_2 = arg_2;
    if (typeof callback === 'function') 
    {
        callback(args);
    }
}

callbackFunction(3, {"name":"James"} , function(result){
    console.log(result);
    //arg_1:3
    //arg_2:{name: 'James'}
})
</code></pre>
    </article>

    <article class="code">
        <h3 id="promise">Promise Function</h3>
        <pre v-highlightjs><code class="hljs javascript">const getDataPromise = () =>
{
    return new Promise(function(resolve, reject) 
    {
        //$.get('url 주소/products/1', (response)=> {
        //     if (response) {
        //     resolve(response);
        //   }
        //   reject(new Error("Request is failed"));
        // });
        const data = {"price":100};
        if(true) resolve(data);
        else reject(new Error("Something Wrong happened!"))
    });
}
            
getDataPromise().
then(function(resolvedData) 
{
    const _item = {"item":"new Car", ...resolvedData}
    return _item 
}).
then(function(item)
{
    const _item = {"color":"Orange", ...item}
    console.log(_item); // {color: 'Orange', item: 'new Car', price: 100}
}).
catch(function(error)
{
    console.log(error); 
});

//Other Case

get_json_request_to_promise('/api/somefoler/any-filename', new FormData())
.then(json => console.log(json));

//{message: 'OK', data: 'abcd:https://aaaa....net/api/login/get-bbbbb?key=46af0edfc0cb3d097170', 
//clientId: '46af0edfc0cb3d097170', time: 300, code: 100}

const get_json_request_to_promise = function(url, formData, method = 'POST',  custom_headers = {})
{
    let param = {
        method: method, // *GET, POST, PUT, DELETE, etc.
        mode: 'cors', // no-cors, cors, *same-origin
        cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
        credentials: 'include', // include, *same-origin, omit
        headers: custom_headers,
        redirect: 'follow', // manual, *follow, error
        referrer: 'no-referrer' // no-referrer, *client
    };

    if (false === (formData instanceof FormData))
    {
        formData = JSON.stringify(formData, null, 2);
    }

    if (!method.match(/GET|HEAD/i)) param.body = formData; // body data type must match "Content-Type" header

    return new Promise(function(resolve, reject) {
        fetch(url, param).then((response)=>{
            if (response.ok)
            {
                resolve(response.json());
            } 
            else reject(new Error(response))
        });
    });
};

</code></pre>
    </article>

    <article class="code">
        <h3 id="async">Async & Await Function</h3>
        <span><a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/await" target="_blank">https://developer.mozilla.org/</a></span>
        <pre v-highlightjs><code class="hljs javascript">const asyncFunction = async (color) =>
{
    let promise = new Promise((resolve, reject) => 
    {
        const _item = {"item":"new Phone"};
        _item.color = color;
        setTimeout(() => resolve(_item), 1000);
    });
    let result = await promise; // 프라미스가 이행될 때까지 기다림 (*)
    return (result); // {item: 'new Phone', color: 'Blue'}
}

asyncFunction("Blue").then(function(_result)
{
    console.log(_result);
});

- async가 붙은 함수는 반드시 프라미스를 반환하고, 프라미스가 아닌 것은 프라미스로 감싸 반환합니다. 
- 또 다른 키워드 await는 async 함수 안에서만 동작합니다.            
</code></pre>
    </article>
<!----------------->
    <article class="code">
        <h3 id="filter">Array.prototype.filter()</h3>
        <pre v-highlightjs>
            <code class="hljs javascript">// filter() 메서드는 주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환합니다.                

const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]

</code></pre>
    </article>

<!----------------->
<article class="code">
    <h3 id="private">Private Field </h3>
    <pre v-highlightjs>
        <code class="hljs javascript">class BankAccount
{
// private으로 선언된 변수
    #balance
    constructor()
    {
        this.#balance = 0;

    }
    // 아래 return을 통해 public으로 선언된 "getter"
    getBalance() {
        const _tempBlance = this.#changeCost(this.#balance);
        return _tempBlance;
    }

    #changeCost(beforeBalance) {
        return beforeBalance * 0.8;
    }

    // 아래 return을 통해 public으로 선언된 "setter"
    setBalance(amount) {
        // ... balance를 업데이트하기 전 검증로직
        this.#balance = amount;
    }
}

const account = new BankAccount();
account.setBalance(100);
console.log(account.getBalance());
console.log(account.#balance);

</code></pre>
    </article>

<!----------------->
<article class="code">
    <h3 id="assert">console.assert()</h3>
    <pre v-highlightjs>
        <code class="hljs javascript">//console.assert(assertion, obj1 [, obj2, ..., objN]);
//assertion - 아무 불리언 표현식. 거짓인 경우, 메시지를 콘솔에 출력합니다. 

const errorMsg = 'the # is not even';
for (let number = 2; number &lt;= 5; number += 1) {
    console.log('the # is ' + number);
    console.assert(number % 2 === 0, {number: number, errorMsg: errorMsg});
    // or, using ES2015 object property shorthand:
    // console.assert(number % 2 === 0, {number, errorMsg});
}
// output:
// the # is 2
// the # is 3
// Assertion failed: {number: 3, errorMsg: "the # is not even"}
// the # is 4
// the # is 5
// Assertion failed: {number: 5, errorMsg: "the # is not even"}
</code></pre>
    </article>

<!----------------->
<article class="code">
    <h3 id="ajax">ajax - vanilla JS</h3>
    <pre v-highlightjs>
        <code class="hljs javascript">//No jQuery
const formData = new FormData();
formData.append('no', 50);
formData.append('eventNo', 31);
urlRequest('/api/gift/get-info', formData, (result) =>
{
    if(result.code === 100)
    {
        console.log("do Something")
    }
    else
    {
        if(result.code === 400)
        {
            console.log(result)
        }
    }
});  

const urlRequest = (url, formData, callback) =>
{
    const obj_data = {};
    /* 만약 formdata를 넘기지 않을 경우를 방지하기 위해 formdata인지를 검사하는 것 */
    if(formData instanceof FormData)
    {
        formData.forEach((value, key) =>
        {
            if (0 == value.length) return;

            if (!Reflect.has(obj_data, key))
            {
                obj_data[key] = value;
                return;
            }
            if (!Array.isArray(obj_data[key]))
            {
                obj_data[key] = [obj_data[key]];
            }

            obj_data[key].push(value);
        });
    }

    const httpRequest = new XMLHttpRequest();
    httpRequest.open('POST', url, true);
    /* Response Type을 Json으로 사전 정의 */
    httpRequest.responseType = "json";
    /* 요청 Header에 컨텐츠 타입은 Json으로 사전 정의 */
    httpRequest.setRequestHeader('Content-Type', 'application/json');
    /* 정의된 서버에 Json 형식의 요청 Data를 포함하여 요청을 전송 */
    httpRequest.send(JSON.stringify(obj_data));
    /* httpRequest의 readyState가 변화했을때 함수 실행 */
    httpRequest.onreadystatechange = () => {
        if (httpRequest.readyState === XMLHttpRequest.DONE) {
            if (httpRequest.status === 200) {
                const result = httpRequest.response;
                if(result)
                {
                    if (typeof callback === 'function') 
                    {
                        callback(result);
                    }
                }
            } 
            else
            {
                const error_result = {};
                error_result.code = 400;
                error_result.status = httpRequest.status;
                error_result.message = "httpRequest Error"
                if (typeof callback === 'function') 
                {
                    callback(error_result);
                } 
            }
        }
    };
};

/* 같은 도메인 내에서만 urlRequest 달리 브라우저만으로 사용가능 formData는 new FormData() 임 */
const fetchRequest = (method, url, formData, callback, custom_headers) =>
{
    let headers = {
        //'Content-Type': 'application/json',
        'Content-Type': 'application/x-www-form-urlencoded',
    };

    if ("object" === typeof custom_headers && custom_headers !== null)
    {
        headers = custom_headers;
    }

    let param = {
        method: method, // *GET, POST, PUT, DELETE, etc.
        mode: 'cors', // no-cors, cors, *same-origin
        cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
        credentials: 'include', // include, *same-origin, omit
        headers: headers,
        redirect: 'follow', // manual, *follow, error
        referrer: 'no-referrer' // no-referrer, *client
    };

    if (false === (formData instanceof FormData))
    {
        formData = JSON.stringify(formData, null, 2);
    }

    const payload = new URLSearchParams(formData);
    //if (!method.match(/GET|HEAD/i)) param.body = formData; // body data type must match "Content-Type" header
    if (!method.match(/GET|HEAD/i)) param.body = payload;

    return fetch(url, param).then(function(response)
    {
        if (response.ok) return response.json();

        throw new Error('Network response was not ok.');

    }).then(function(json)
    {
        if(callback) callback(json);
        return json;
    });
};
</code></pre>
    </article>

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
