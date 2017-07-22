## fetch用法说明
---
#### 语法说明
```js
fetch(url, options)
  .then(res => {
    // handlle HTTP response
  }, error => {
    // handle network error
  })
```

##### url
- `USVString`字符串，包含要获取资源的`URL` 或者 `Request`对象


#### options (可选)
- `method`: 请求使用的方法， 如 `GET` `POST`
- `headers`: 请求的头信息， 形式为`Headers`对象或`ByteString`
  - `body`: 请求的`body`信息: `Blob`, `BufferSource`, `FormData`, `URLSearchParams`, `USVString` (注意: `GRT` 或 `HEAD` 方法的请求不能包含`body`信息)
  - `mode`: 请求的模式， 如 `cors`, `no-cors`, `same-origin`
  - `credentials`: 请求的`credentials`， 如 `omit`, `same-origin`, `include`
  - `cache`: 请求的`cache`模式： `default`, `no-store`, `reload`, `no-cache`, `force-cache`, `only-if-cached`
