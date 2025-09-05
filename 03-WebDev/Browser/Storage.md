#浏览器存储
常见的浏览器存储方式：
- `cookie`
- `Web Storage API(localStorage,sessionStorage)`
- `indexedDB`
## Cookie：
Cookie 本质上就是存储在**浏览器本地**的一个很小的文本文件，内部表现为**键值对**的形式。再发送请求的时候，cookie会被自动附在请求头里。
### 属性：
- `key`：键名
- `value`：值
- `expire`：过期时间。一旦过期浏览器自动删除cookie。如果不设置过期时间，则cookie有效期是会话期间。
- `secure`：当 secure 属性设置为 true 时，cookie 只有在 https 协议下才能上传到服务器（http不可以❌）
- `path`：==限制路径==指定 Cookie 有效的 URL 路径前缀，只有在请求路径 **匹配这个前缀**时，才会带上 Cookie
- `domain`：==限制域名== 设置了 `Domain`：该域和它的子域都能带上这个 Cookie。
---
### 缺陷：
- 容量有限：大小限制4K
- 性能缺陷：不管域名下面的某一个地址需不需要这个 Cookie ，请求都会携带上完整的 Cookie。在请求头中额外附加内容会带来流量消耗和性能浪费。
- 安全缺陷。由于 Cookie 以纯文本的形式在浏览器和服务器中传递，很容易被非法用户截获、篡改，在 Cookie 的有效期内重新发送给服务器。
---
### 跨域：
为了实现跨域 Cookie 共享，服务器需要设置 `Access-Control-Allow-Credentials` 为 true，并且 `Access-Control-Allow-Origin` 不能使用 `*`，**必须指定具体的域名**。同时，客户端请求时需要携带 `credentials: 'include'` 或者在 XMLHttpRequest 中设置 `withCredentials = true`;
***
## Web Storage：
将数据存储在浏览器本地。
### API：
- `setItem(key, value)`：保存键值对，同名则覆盖
- `getItem(key)`：获取对应的值，没有则返回`null`
- `removeItem(key)`：删除某个键
- `clear()`：清空storage
- `length`：获取storage的键值对总数
**Storage的操作都是==同步的==**
### localStorage：
持久存储，所有同源窗口共享 -> **所有同源的标签页共享同一份`localStorage`数据**。
当一个同源窗口对 `localStorage` 进行修改时，其他同源窗口会收到 **`storage` 事件** -> 可以通过`eventListener`进行捕获。
### sessionStorage：
仅在当前窗口/标签页的会话中有效，窗口关闭就没了。
***
## indexedDB：
是一种底层 API，用于在客户端存储大量的结构化数据。本质上是一个非关系型数据库。
