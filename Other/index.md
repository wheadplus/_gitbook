# 其他

## gitbook

常用命令

```js
gitbook serve 启动服务
gitbook init 根据SUMMARY.md的结构初始化目录
gitbook build 生成网页
```





## 提交

1. 提交源码
```
git add .
git commit -m '提交说明'
git push git@github.com:wheadplus/gitbook.git
```

2. 部署gh-pages
```
cd _book
git add .
git commit -m '提交说明'
git push git@github.com:wheadplus/gitbook.git  gh-pages
```

