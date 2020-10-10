
## GitCodeTree

fork from [https://github.com/buunguyen/octotree](https://github.com/buunguyen/octotree)

## 安装
### 从预先构建的包安装(适用于所有浏览器)
 **鉴于国内墙的原因，你可以通过下载已经构建好的包来安装**

预先构建的包可以从 [https://gitee.com/oschina/GitCodeTree/tree/master/dist](https://gitee.com/oschina/GitCodeTree/tree/master/dist) 下载。出于安全原因，请不要从其它地方下载。

__注意__: Firefox 43 + 需要签名。因此您需要从Mozilla商店安装GitCodeTree。出于某种原因,如果你想安装预先构建的包，请参考 [disable sign-check](https://github.com/buunguyen/octotree/issues/220#issuecomment-166012724)。

### 在 Chrome, Firefox 和 Opera 上安装
* 从 [Chrome Web Store](https://chrome.google.com/webstore/detail/gitcodetree/inaaldjpdbkaodlmdcplgpoibohcmmlj)，[Mozilla Add-ons Store](https://addons.mozilla.org/zh-CN/firefox/addon/giteetree/) or [Opera Add-ons Store](https://addons.opera.com/en/extensions/details/gitcodetree/) 安装GitCodeTree
* 导航到任何Gitee、GitHub库(或者刷新这个页面作为一个例子)
* 代码树将显示在页面左边

### 在 Safari 上安装

GitCodeTree在Safari gallery中不可用；所以，您必须使用预先构建的包 或者 从源代码构建一个。

* 下载 [Safari 预先构建的包](https://gitee.com/oschina/GitCodeTree/blob/master/dist/safari.safariextz?raw=true)
* 双击或者拖拽到Safari窗口

## 介绍

浏览器插件 (Chrome, Firefox, Opera and Safari) 在Gitee、GitHub上显示代码树。不用clone到本地就能查看项目结构. 特性:

* 就像在IDE一样简单易用的代码树
* 快速浏览文件，不刷新页面
* 支持私人存储库 (Gitee登录后就可查看， Github 需要填写[access_token](#access-token))

![GitCodeTree on Gitee](docs/chrome-gitee.png)
![GitCodeTree on GitHub](docs/chrome-github.png)

### 二次开发

* 将项目clone到本地
* 在`src/adapters/`中为你想要支持的网站添加一个类(可复制`src/adapters/github.js`并修改)
* 根据情况实现 [`_getTree`](https//gitee.com/inu1255/GitCodeTree/blob/master/src/adapters/github.js#L149-154) 或 `_get` 方法，用于获取项目树
* 实现 [`updateLayout`](https//gitee.com/inu1255/GitCodeTree/blob/master/src/adapters/github.js#L65-73) 方法，用于修改页面布局
* 实现 [`selectFile`](https//gitee.com/inu1255/GitCodeTree/blob/master/src/adapters/github.js#L135-138) 指定pjax替换的html元素，用于不刷新切换文件
* 在 [`src/octotree.js`](https//gitee.com/inu1255/GitCodeTree/blob/master/src/octotree.js#L30)中添加你修改好的类
* 在 `src/config/` 插件配置文件中添加你想要支持的网站
* __chrome中调试__: 使用`gulp chrome`命令，打开[chrome://extensions/](chrome://extensions/)，点击`加载已解压的扩展程度`，选择`src/tmp/chrome`
* __打包__: 使用 `gulp dist` 命令打包

## 设置
### Access Token

__注意__: GitCodeTree 访问令牌在浏览器本地存储并不会上传到任何地方。如果你想验证,查看源代码，开始 [请参考这里](https//gitee.com/inu1255/GitCodeTree/blob/master/src/view.options.js#L77).

#### GitHub
GitCodeTree 使用 [GitHub API](https://developer.github.com/v3/) 检索代码树。默认情况下，它使未经身份验证的请求到GitHub API。然而，有两种情况时必须经过身份验证的请求:

* 你访问一个私人存储库
* 你超过 [请求频率限制限制](https://developer.github.com/v3/#rate-limiting)

当这种情况发生时，GitCodeTree会询问你 [GitHub 私人 access token](https://help.github.com/articles/creating-an-access-token-for-command-line-use). 如果你没有，[点此创建](https://github.com/settings/tokens/new)， 然后复制粘贴到文本框中。注意，至少要允许"public_repo"，"repo" (如果你需要访问私人仓库).

![Settings](docs/settings.jpg)

### 其它
* __热键__: GitCodeTree 使用 [keymaster](https://github.com/madrobby/keymaster) 注册热键。查看 [支持的按键](https://github.com/madrobby/keymaster#supported-keys).
* __记得栏可见性__: 如果勾选此项，基于其可见性显示或隐藏GitCodeTree.
* __在非代码页__: 如果勾选此项，让GitCodeTree等非代码页的问题和请求.
* __一次加载整个树__: (仅支持github) 如果勾选此项，进入项目页面时GitCodeTree将加载整个项目树。如果您经常访问非常大的项目，为了避免长时间加载，请勿勾选此项.
