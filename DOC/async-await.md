# async
## async 含义
> 有一种特殊的语法可以更舒适地与promise协同工作，它叫做async/await
## Async functions
> async关键字: 它被放置在一个函数前面。就像下面这样
```
async function f() {
    return 1
}
```
> 函数前面的async一词意味着一个简单的事情：这个函数总是返回一个promise，如果代码中有return <非promise>语句，JavaScript会自动把返回的这个value值包装成promise的resolved值
```
async function f() {
    return 1
}
f().then(alert) // 1
```
## await (只能在async函数内部使用)
> 关键词await可以让JavaScript进行等待，直到一个promise执行并返回它的结果，JavaScript才会继续往下执行。
```
async function f() {
    let promise = new Promise((resolve, reject) => {
        setTimeout(() => resolve('done!'), 1000)
    })
    let result = await promise // 直到promise返回一个resolve值（*）
    alert(result) // 'done!'
}
f()
```
## 错误处理
> 如果一个promise正常resolve，那么await返回这个结果，但是在reject的情况下会抛出一个错误，就好像在那一行有一个throw语句一样
```
async function f() {
    await Promise.reject(new Error('whoops!'))
}
// 同下
async function f() {
    throw new Error('Whoops!')
}
```
## async 作用
> 放在一个函数前的async有两个作用：
```
1.使函数总是返回一个promise
2.允许在这其中使用await
```
> promise前面的await关键字能够使JavaScript等待，直到promise处理结束。然后
```
1.如果它是一个错误，异常就产生了，就像在那个地方调用了throw error一样。
2.否则，它会返回一个结果，我们可以将它分配给一个值
```
> 他们一起提供了一个很好的框架来编写易于读写的异步代码