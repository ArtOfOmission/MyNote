# json

## 1. JSON对象
### 1.1 JSON.stringify()
```javascript
let json = {
    a: 12,
    b: 34
};
let str = 'https://cn.bing.com/path/user:data=' + encodeURIComponent(JSON.stringify(json));
console.log(str);
```
### 1.2 JSON.parse()
```javascript
let str2 = '{"a":12,"b":23,"c":34}';
let json2 = JSON.parse(str2);
console.log(json2);
```

## 2. 简写(名字一样)、方法

### 2.1 简写（名字跟值一样时(key和value)）
```javascript
let a = 12;
let b = 5;
// let json3 = {
//     a: a,
//     b: b
// };
let json3 = {
    a,
    b,
    c: 33
};
console.log(json3);
```
### 2.2 方法简写
```javascript
// let json4 = {
//     a: 12,
//     show: function () {
//         console.log(this.a);
//     }
// }
let json4 = {
    a: 12,
    show() {
        console.log(this.a);
    }
}
json4.show();
```

## 注：json的标准写法：
1. 只能用双引号
2. 所有的名字都必须用引号标起来
```javascript
    {a: 12, b:5}//错误
    {"a": 12, "b": 5}//正确
    {a:'abc', b: 5}//错误
```