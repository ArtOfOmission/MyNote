# 几种常见的CSS布局

## 1.流体布局
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>流体布局</title>
    <style>
        .left {
            float: left;
            width: 100px;
            height: 200px;
            background: red;
        }

        .right {
            float: right;
            width: 200px;
            height: 200px;
            background: blue;
        }

        .main {
            margin-left: 120px;
            margin-right: 220px;
            height: 200px;
            background: green;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="left"></div>
        <div class="right"></div>
        <div class="main"></div>
    </div>

</body>

</html>
```

## 2.圣杯布局
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>圣杯布局</title>
    <style>
        .container {
            margin-left: 120px;
            margin-right: 220px;
        }

        .main {
            float: left;
            width: 100%;
            height: 300px;
            background: green;
        }

        .left {
            position: relative;
            left: -120px;
            float: left;
            height: 300px;
            width: 100px;
            margin-left: -100%;
            background: red;
        }

        .right {
            position: relative;
            right: -220px;
            float: right;
            height: 300px;
            width: 200px;
            margin-left: -200px;
            background: blue;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="main"></div>
        <div class="left"></div>
        <div class="right"></div>
    </div>

</body>

</html>
```

## 3.双飞翼布局
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>双飞翼布局</title>

    <style>
        .content {
            float: left;
            width: 100%;
        }

        .main {
            height: 200px;
            margin-left: 110px;
            margin-right: 220px;
            background: green;
        }

        .main::after {
            content: '';
            display: block;
            font-size: 0;
            height: 0;
            zoom: 1;
            clear: both;
        }

        .left {
            float: left;
            height: 200px;
            width: 100px;
            margin-left: -100%;
            background: red;
        }

        .right {
            float: right;
            height: 200px;
            width: 200px;
            margin-left: -200px;
            background: blue;
        }
    </style>
</head>

<body>
    <div class="content">
        <div class="main"></div>
    </div>
    <div class="left"></div>
    <div class="right"></div>
</body>

</html>
```