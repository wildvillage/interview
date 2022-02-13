# 2-13 面试题

## 一、全排列

```js

const _permute = string => {
  let charArr = string.split('');
  let res = [];
  process(charArr, 0, res)
  return res
}
function process(charArr, i, res) {
  if (i === charArr.length) {
    res.push(charArr.join(''))
    return
  }
  for (let j = i; j < charArr.length; j++) {
    change(charArr, j, i);
    process(charArr, i + 1, res);
    change(charArr, j, i);
  }
}
function change(arr, i, j) {
  if (i === j) return;
  let tmp = arr[i];
  arr[i] = arr[j];
  arr[j] = tmp;
}

```


利用递归实现，核心就是尝试；在每一个位置都进行尝试；比如第一个0位置每一个元素都可以来到该位置尝试，子规模再在剩下的部分进行尝试；

## 二、手写instanceof
    

```js

const _instanceof = (target, Fn) => {
  if (Fn.prototype === target.__proto__) {
    return true;
  }
  let proto = Fn.prototype;
  while (proto) {
    if (proto === target.__proto__) {
      return true;
    }
    proto = proto.__proto;
  }
  return false
}

```

instanceof是判断某个实例对象是否是目标构造函数的实例，如果是的话，那么实例对象一定可以通过若干个__proto__指向目标的原型对象；所以得到上面的函数；


## 三、 实现一个.call方法

```js

Function.prototype._call = function (context, ...rest) {
  context.fn = this;
  return context.fn(...rest)
}

```

实现.call方法的核心就是函数的调用方式会影响函数内部this的指向；如果函数是通过对象.的方式调用的，那么函数内部的this会指向该对象；