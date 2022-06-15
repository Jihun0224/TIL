# 동기와 비동기 방식
![image](https://user-images.githubusercontent.com/59672592/173753650-9867f340-6c46-4914-9c1b-f11fc9cc36d3.png)

## 동기(Synchronous)
동기식 통신 및 동기 프로그래밍이란 동시에 일어난다는 뜻이다.  
동시에 일어난다는 것은 Request를 보내게 되면 시간이 얼마나 걸리든 그 자리에서 Response를 받는다는 말이다.   
즉, `모든 일은 순차적으로 실행되며 어떤 작업이 수행중이라면 다음 작업은 대기하게 된다.`

```javascript
function func1(){
    console.log('func1');
    func2();
}

function func2(){
    console.log('func2');
    func3();
}

function func3(){
    console.log('func3');
}
func1();
/*
output
func1
func2
func3
*/
```

동기식에서 Request를 보낸 Thread는 Response가 도착하기 전까지는 아무것도 하지 못하는 Block상태가 된다.  
이렇게 되면 해당 Thread는 Request를 보내고 Response를 받고 Request를 다시 보내는 작업을 수행하게 된다. 이를 통해 요청과 응답값의 순서를 보장하게 된다. 또한 보낸 Request에 대한 처리 결과 값을 보장 받을 수 있다.   
이는 요청 값에 대해 성공, 실패 및 처리 결과에 대해 변경되는 사항이 있는 경우, 중요한 요소이다.  
하지만, Response가 지연되게 된다면 Request를 보낸 Thread는 해당 Response를 무작정 기다리는 상태가 된다는 말이기도 하다.  
서버에 가져오는 데이터 양이 늘어날수록 앱의 실행속도는 기하급수적으로 느려진다.

## 비동기(Asynchronous)
비동기식 통신 및 비동기식 프로그래밍이란 동시에 수행하지 않는다는 뜻이다.  
동기식과는 반대로 Request를 보내더라도 Response를 언제 받아도 상관 없다는 말로, Request를 보내고 Response를 상관하지 않는 상태가 되는 것이다.  
Request를 보내고 Response를 기다리지 않고 다른 일을 하는 이러한 상태를 Non Block 상태라고 한다.  

```javascript
function func1(){
    console.log('func1');
    func2();
}

function func2(){
    setTimeout(function(){
        console.log('func2');
    }, 0);
    func3();
}

function func3(){
    console.log('func3');
}
func1();
/*
output
func1
func3
func2
*/
```
Thread가 Response를 받지 않고 여러가지 요청을 보냈을 경우, 뒤에 보낸 요청이 먼저 처리가 되었다면 뒤에 요청값에 대한 응답값이 먼저 올 수 있다. 즉, `ASynchronous 방식은 순서를 보장하지 않는다.`
하지만, 계속 자기일을 하는 ASynchronous방식은 Synchronous방식에 비해 성능적으로 좋을 수 밖에 없다. 다만 Response에 대한 처리 결과를 보장받고 처리해야 되는 서비스에서는 적합하지 않다.

![image](https://user-images.githubusercontent.com/59672592/173756212-4be99a3d-95a7-4f54-998a-d610c18c4023.png)  
<br>

# 자바스크립트로 비동기 프로그래밍
> <h2>자바스크립트는 싱글 스레드 언어이다</h2>

싱글 스레드인 자바스크립트 코드를 실행하면 순차적으로 실행이 된다. 오래걸리는 작업의 실행이 완료될 때까지 그 어떤 작업도 진행되지 않기에, 화면 로딩, 통신, 연결 등의 실행속도는 기하급수적으로 느려진다.  
오늘날같이 많은 이미지와 데이터 요청이 필요한 웹페이지를 실행할 때는 이러한 단점이 더욱 부각될 것이다.

이러한 문제를 해결하기 위해 자바스트립트에서는 비동기적 프로그래밍을 구현할 수 있돌고 다양한 방법을 제공하고 있다. 
## Callback 함수
Callback함수는 특정 함수에 매개변수로 전달된 함수를 의미한다. 그 콜백함수는 함수를 전달받은 함수안에서 호출된다.
```javascript
function Callback(callback){
    console.log('콜백 함수');
    callback();
}
Callback(function(){
    console.log('콜백 받는곳');
})
```
Callback 함수에서는 Callback을 받지 않는다면 함수의 과정이 끝나기도 전에 다음 프로세스를 진행하게 되는 경우가 있다.
또한, 가독성이 좋지 않다.

![image](https://user-images.githubusercontent.com/59672592/173761234-74fe1e85-46c0-41cf-8600-384757a21445.png)

이렇게 미친듯이 중첩된 callback함수를 콜백 지옥이라고 부흔다. 가독성이 매우 떨어지기에, callback지옥 내부에서 어떤 에러가 발생했을 때 찾아내기가 정말 어렵다!
 그래서 ES7에서는 promise를 ES8에서는 async, await를 지원한다.

## Promise
자바스크립트에서 비동기 task를 다룰 수 있게 도와주는 객체로, 비동기적 작업을 하는 함수의 return type으로 사용 된다.

함수 안의 작업이 성공적으로 동작했을 때 동작하는 'resolve' callback과 함수가 동작이 실패해서 에러가 발생했을 때 동작하는 'reject' callback을 인자로 받는 함수를 실행한다.

```javascript
// 기본적으로 PROMISE는 인터페이스와 같으므로 new 생성자를 이용합니다
// Promise는 resolve와 reject에 해당하는 callback 2개를 받는
// 함수를 인자로 받습니다.
let promise = new Promise(function(resolve, reject) {});

//기본예제1
let myFirstPromise = new Promise((resolve, reject) => {  
  setTimeout(function(){
    resolve("Success!"); // resolve callback만 구현한 예제
  }, 250);
});

출처 : MDN
```
Promise는 처음에는 함수가 실행되기를 쭉 기다리고 있는 Pending 상태였다가, 함수가 잘 작동이 되면 resolve 가 되면서 resolve callback을 실행시키며 프로미스를 종료하고, 함수가 작동하다가 에러가 나면 rejected 상태가 되면서 reject callback을 실행한다.

기존 callback 사용시와 차이가 있다면, 기존에는 resolve, reject 각각의 상황에 대응하는 함수를 직접만들어 대입을 했어야 했지만, Promise의 경우 dafault로 resolve, reject callback method가 내장되있어 보다 편리하고 심플하게 사용할 수 있다는 장점이 있다.

> .then(), .catch()

Promise 사용 시 이 두가지를 가지고 callback 지옥없이 연속적으로 비동기적인 동작을 하는 코드를 작성이 가능하다.

`.then()` 의 경우, 앞의 데이터를 받아온 다음에(then) 그 값으로 무언가를 실현한다는 것으로, chaining을 통하여 callback을 구현한 것으로 볼 수 있다.

`.catch()` 의 경우, 앞의 데이터 중 error만을 받아와(catch해) 그 값으로 무언가를 실현하는 것으로, error 상황에 특정한 callback을 구현한다.
```javascript
our_work.then((...) => {
  console.log(...)
  return callback_on_success1()
})
	.then((......) => { //callback_on_success1()의 return 값을 가지고 진행
  console.log(......)
  return callback_on_success2()
})
	.catch(error => {
  console.log(error)
  return reject()
})

출처 : two_jay.log
```
#### ⚠️주의 사항
Promise를 .then으로 체이닝해서 연속적으로 실행 가능하다는 점을 보면 알듯이, Promise는 Promise를 반환한다 (.then과 .catch를 포함한 Promise 관련 메소드들도 포함됨).

⇒ 이로 인하여 위험한 상황이 발생하는데, Promise를 얹고 얹으면서 반환값이 중간에서 꼬여버린다면, 콜백지옥은 코드를 스윽 읽어라도 볼 수 있지만, Promise는 일일히 반환값을 디버거로 뜯어봐야한다..!

중간에 다른 값이 필요할 때에도 callback과 마찬가지로 코드를 읽기 어렵도록 하여 가독성을 해친다.

### async / await
Node.js 7.6버전부터 구현된 기능이며 Async/Await를 사용하면 promise에 비해 보다 쉽게 비동기적인 상황을 표현할 수 있다.
```javascript
async function f1() {
  const a = await add10(10);
  const b = await add10(a);
  console.log(a, b)
}
f1();
```
Async와 Await을 사용하려면 우선 사용할 함수 앞에 async라는 키워드를 붙여 사용해야 하며 선언된 `async 함수 안에서만 await 키워드를 사용할 수 있다.`


이렇듯 async로 "이 함수에는 비동기적으로 실행되는 작업이 포함되어 있습니다"라고 선언하고, 비동기적 실행이 필요한 곳에만 await처리를 함으로서 일반적인 함수 실행/선언 환경처럼 편리하게 비동기 프로그래밍이 가능하다.


# 참고자료
- [비동기 프로그래밍. 왜 하죠?](https://velog.io/@two_jay/callback-%EA%B3%BC-%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)
- [깜찍한 프로그래머들을 위한 간단한 프로그래밍 상식(3. 비동기식 프로그래밍 async in js; callbackhell-promise-async로 ..)](https://medium.com/@curnqke/%EA%B9%9C%EC%B0%8D%ED%95%9C-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EB%93%A4%EC%9D%84-%EC%9C%84%ED%95%9C-%EA%B0%84%EB%8B%A8%ED%95%9C-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%EC%83%81%EC%8B%9D-3-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%8B%9D-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-async-in-js-95339f10a4d6)