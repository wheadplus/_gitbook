### `HTTP` 缓存有那几种？

#### 无缓存

每次都要重新请求文件，如果文件大，变更少。很浪费带宽。

#### 缓存

请求资源，把资源缓存在本地，如果调用直接从本地获取。

但是：

- 节省带宽
- 如果文件更新，浏览器本地不更新

#### Expires(过期)（缓存+更新机制）

在缓存的基础上加个(Expires)过期时间,如果时间过期，则重新请求资源。

但是：

- 缓存可控制
- 过期时间需对比本地时间
- 控制单一

#### CacheControl（缓存+更新机制2.0）

更新机制`1.0`版本只有 `expires`,更新机制`2.0`更多参数。

```
Cache-Control: max-age=300
Cache-Control: max-stale[=<seconds>]
Cache-Control: min-fresh=<seconds>
Cache-control: no-cache 
```

[详细参数说明看MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)

但是还能优化：

- 如果时间过期了，重新想服务器请求文件，发现文件未修改，则无需更新文件，只需打回消息（文件未更新即可）

#### ETag

#### 更新机制3.0，增加参数ETag,如果ETag未修改则无需更新文件。

```
Cache-Control: max-age=300；
ETag:W/"e-cbxLFQW5zapn79tQwb/g6Q"
```



## 参考

[参考1](https://zhuanlan.zhihu.com/p/23299600?refer=study-fe)

[参考2](https://imweb.io/topic/5795dcb6fb312541492eda8c)