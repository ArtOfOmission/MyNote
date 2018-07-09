# Promise--承诺

> 异步：操作之间没什么关系，同时进行多个操作<br>
> 同步：同时只能做一件事

> 异步：代码更复杂<br>
> 同步：代码简单

## 1. Promise--可以消除异步操作 
*用同步一样的方式，来书写异步代码*

### 实例1

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>promise</title>
    <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
    <script>
        let p = new Promise(function (resolve, reject) {
            //异步代码
            //recolve--成功
            //reject--失败
            //alert(resolve);
            $.ajax({
                url: 'data/array.txt',
                dataType: 'json',
                success(arr) {
                    resolve(arr);
                },
                error(err) {
                    reject(err);
                }
            });
        });
        p.then(function (arr) {
            alert('success' + arr);
        }, function (err) {
            console.log(err);
            alert('error' + err);
        });
    </script>

</head>

<body>

</body>

</html>
```

### 实例2

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>promise</title>
    <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
    <script>
        function createPromise(url) {
            return new Promise(function (resolve, reject) {
                $.ajax({
                    url,
                    dataType: 'json',
                    success(arr) {
                        resolve(arr);
                    },
                    error(err) {
                        reject(err);
                    }
                });
            });
        }

        Promise.all([
                createPromise('data/array.txt'),
                createPromise('data/json.txt')
            ])
            .then(function (arr) {
                let [res1, res2] = arr;
                alert("全部成功！");
                console.log(res1,res2); 
            }, function () {
                alert("至少有一个失败了！");
            });

    </script>

</head>

<body>

</body>

</html>

```

### 实例3

#有了promise之后的异步#
```javascript
 Promise.all([$.ajax(),$.ajax()]).then(results => {
            alert('获取成功！');        
        }, err => {
            alert('失败了！');
        });
```

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
    <script>
        Promise.all([
            $.ajax({
                url: 'data/array.txt',
                dataType: 'json'
            }),
            $.ajax({
                url: 'data/json.txt',
                dataType: 'json'
            })
        ]).then(function (results) {
            let [arr, json] = results;
            console.log(arr,json); 
        }, function () {
            alert('失败了！');
        });
    </script>
</head>

<body>

</body>

</html>
```

## 2. promise.race
```javascript
 Promise.race([
     $.ajax(),
     $.ajax(),
     $.ajax(),
     $.ajax()
     ]);
```
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
    <script>
        Promise.all([
            $.ajax({
                url: 'data/array.txt'
            }),
            $.ajax({
                url: 'data/json.txt'
            }),
            $.ajax({
                url: 'data/num.txt'
            })
        ]).then(result => {
                let [arr, json, num] = result;
                alert('成功！');
                console.log(arr, json, num);
            },
            err => {
                alert('失败！');
            }
        );
    </script>
</head>

<body>

</body>

</html>
```


