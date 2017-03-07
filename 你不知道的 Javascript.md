####作用域

词法作用域：编译阶段确定（欺骗词法作用域 eval with）
```
function foo(str){
  "use strict"
  eval(str)
  console.log(a)
}
foo('var a = 2')
function foo(obj){
  with (obj){
    a = 2
  }
}
var o1 = {a:3}
var o2 = {b:3}
foo(o1)
foo(o2)
```

### 块作用域 with try/catch let const
for (let i=0; i<10; i++){
  console.log(i)
}
if (true) {
  var a = 1
  let b = 2
  const c = 3
}
console.log(a) // 1
console.log(b) // ReferenceError
console.log(c) // ReferenceError
try{throw 2}catch(a){
  console.log(a) // 2
}
console.log(a) // ReferenceError
提升
定义提升 函数优先
foo() // TypeError
bar() // ReferenceError
var foo = function bar(){}
foo() // 1
function foo(){
  console.log(1)
}
foo = function(){
  console.log(2)
}
foo() // 3
function foo(){
  console.log(1)
}
foo = function(){
  console.log(2)
}
function foo(){
  console.log(3)
}
// 这种语法在最新版浏览器已经被摒弃并且报错，函数在 if 中类似 let 拥有一个局部作用域
foo() // 2
if (true){
  function foo(){console.log(1)}
}else{
  function foo(){console.log(2)}
}
