|           |                 Call                 |                Apply                 |                  Bind                   |
| --------- |:------------------------------------:|:------------------------------------:|:---------------------------------------:|
| Execution |        At the time of binding        |        At the time of binding        | At the time when we execute the return  |
| Parameter |        Any numbers one by one        |                  []                  |     [] and any number of arguments      |
| Is Return | Yes, and call at the time of binding | Yes, and call at the time of binding | Yes, it returns a copy of the function' |

```js
var obj = { num: 2 }

var add = function(a, b) {
	return this.num + a + b;
}
```


```js
add.call(obj, 3, 1);
```

```js
add.apply(obj, [3, 1]);
```

```js
var bound = add.bind(obj);
bound(3, 1);
```