# 一些零散的关于React / Typescript的知识

### this指向
一个很好的帖子：https://www.cnblogs.com/pssp/p/5216085.html
必须要说的是，*this的指向在函数定义的时候是确定不了的*，只有函数执行的时候才能确定this到底指向谁，**实际上this的最终指向的是那个调用它的对象**
举例：

```javascript
function fn(a,b,c) {
    return a + b + c + this.d;
}
fn(1,2,3) // undefined
```
我们就去定义一个上级对象：
```
var o = {d: 4, f:fn}
o.f(1,2,3) // 10
```

### bind()函数
一个很好的帖子https://www.webhek.com/post/javascript-bind.html
了解了this指向后，就深入了解一下bind函数。**首先要明白，bind()是个函数，调用它会创建一个新的函数**。  
当这个新函数被调用时，它的 this 值是传递给 bind() 的第一个参数, 它的参数是 bind() 的其他参数和其原本的参数。
继续拿上面的fn举个例子
```
var bfn = fn.bind({'d':4}, 1,2,3)
bfn() // 10
```
