# Promise--承诺

> 异步：操作之间没什么关系，同时进行多个操作<br>
> 同步：同时只能做一件事

> 异步：代码更复杂<br>
> 同步：代码简单

## Promise--可以消除异步操作
*用同步一样的方式，来书写异步代码*
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
        }, function () {
            alert('error');
        });
    </script>

</head>

<body>

</body>

</html>
```


