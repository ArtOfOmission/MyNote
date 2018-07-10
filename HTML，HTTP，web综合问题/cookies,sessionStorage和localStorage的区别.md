# cookies,sessionStorage和localStorage的区别

- 1.cookie是为了标识用户身份而储存的用户本地终端（client side）上的数据（通常经过加密），cookie数据通常会在同源的http请求中携带（即使不需要），即会在浏览器和服务器间来回传递

- 2.sessionStorage和localStorage，仅保存在本地

- 3.存储大小
    - 3.1 cookie数据大小不能超过4K
    - 3.2 sessionStorage和localStorage虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大

- 4.有效期
    - 4.1 localStorage 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据
    - 4.2 sessionStorage 数据在当前浏览器窗口关闭后自动删除
    - 4.3 cookie 设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭