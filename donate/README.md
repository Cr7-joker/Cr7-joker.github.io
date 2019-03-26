# Donate-Page simple

![GIF动态效果图](https://upload-images.jianshu.io/upload_images/1819713-518ef42c3301b2fa.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/420/format/webp)

#### 直接 Fork 之后需要修改以下内容为你的账户

```
/script.js:4-6 对应账户的二维码路径
/index.html:28 PayPal.me 改为现在收款页面，这样可以删除原来的按钮方式了。
```

#### 针对不同项目可以直接在 URL 加入项目参数和金额，不过仅仅作用于 PayPal 方式.

```
https://cdn.rawgit.com/TinyJay/donate-page/6fe4f885/simple/?item='donate-page&price=2'
```

#### 使用 `iframe` 嵌入页面的代码，高度至少 `240px`，宽度至少 `310px`！

```
<iframe src="https://rawcdn.githack.com/TinyJay/donate-page/51aaf216f048b8e6d5ce01443a32be930b91869d/simple/index.html" style="overflow-x:hidden;overflow-y:hidden; border:0xp none #fff; min-height:240px; width:100%;"  frameborder="0" scrolling="no"></iframe>
```

### License

Released under the MIT license.
