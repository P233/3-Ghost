# 3-Ghost Theme

DEMO: [http://peiwen.lu](http://peiwen.lu)

欢迎任何改进建议，请直接[提交 issues](https://github.com/P233/3-Ghost/issues/new)，感谢。

## 主要功能

* 不支持 IE9 及以下浏览器。
* 三列布局，最左侧是博客的 Tags 列表（需手动配置），点击后过滤相关文章，一篇文章可以给多个 tags 不会影响。
* 使用 [prism.js](http://prismjs.com) 代码高亮。
* 支持插入 Codepen。
* Lazy-load Disqus。
* 自动生成文章目录列表（h1-h3），鼠标移动到浏览器右侧边缘自动滑出，目前对中文支持不好（详见已知问题 #2）。
* 支持移动设备，文章目录在移动设备上不显示。

同时制作了一份 Jekyll 版本，请查看：[https://github.com/P233/3-Jekyll](https://github.com/P233/3-Jekyll)，你也可以移植给其他 Blog 平台，需遵守 MIT License。

**安装后需要做一些简单配置才可使用，请仔细阅读下面的说明：**

## 配置模板

首先，启用这款模板后请务必在 Ghost 后台 `/ghost/settings/general/` 页面将 “Posts per page” 设置为 `999` 或 `9999`。

### 模板文件

`default.hbs` 包含整个页面框架，以及左侧 sidebar 部分；`index.hbs` 仅包含首页内容；`post.hbs` 包含文章内容，分享按钮，以及评论等等。

### 设置标签

这是修改模板最关键的一步。

1. 打开 `default.hbs` 文件找到 `<ul id="tags__ul"></ul>` 部分，将 `place_your_tag_display_name_here` 替换成 Tag 显示名称，别忘记修改 ID 顺序，完毕之后记录 tags 顺序以及总数。
2. 打开 `/assets/js/script.js` 找到 `// Variables` 部分，将 `place_your_tag_name_here` 替换成 tag 名称，这个名称需要与 Ghost 编辑文章时输入的 tag 一模一样，同时也需要满足 CSS 的 class 命名规则（不得已会影响命名 tag 的方式），顺序要与第一步匹配。
3. 在 js 文件中继续寻找 `// Tags switcher` 注释后面跟着的 `for`  循环，将 `i <= 6` 换成 tags 总数 + 1 (因为 No.1 是全部分类)。

### 搜索功能

搜索框目前只是摆设，请等待 Ghost 加入搜索功能，或者使用 [Google Custom Search Engine](https://www.google.com/cse/)。

### 修改头像

没有用到 Ghost 后台的头像上传功能，需替换 `/assets/img/` 中的头像图片，`100px * 100px` 用于普通屏幕， `200px * 200px` 用于 Retina Display。

### 修改邮箱

很抱歉也没使用 Ghost 的后台邮箱地址，而是通过 [Stop Link Spam Bots](http://www.safeemail.org/) 编辑了一下手动粘贴，希望能防 spam。

### Icon-font

使用了 [Fontello icon fonts generator](http://fontello.com)，并附上了 config 文件放置在 `/assets/font/` 中，方便替换图标。

### 代码高亮

代码高亮使用的是 [prism.js](http://prismjs.com)。js 放在 `/assets/js/prism.js` 中，已包含的语言包有 `Markup` `CSS` `CSS Extras` `C-like` `JavaScript` `SCSS` 以及 `Bash`，如果需要支持其他语言请直接替换这个文件。模板使用的是修改过的 COY，放在 `/assets/_sass/_prism.scss` 中。

补充一点 Ghost 中使用 prism 高亮代码的方法，输入代码时在 ` ``` ` 后紧跟 `language-*`。Ghost 会自动将后者添加给 `<pre>` 标签作为 classname，如下图

![](http://peiwen.lu/content/images/2013/Dec/mdhl.gif)

### Embedding Codepen

如果需要插入 Codepen，只需将 embed code 中的 `<p>` 标签粘贴在正文中，而不必粘贴 `<script>` 标签。更多关于插入 Codepen 的解释请查看 http://blog.codepen.io/documentation/features/how-do-i-embed-a-pen-on-another-site/ 。

如果完全不需要这个功能可以将 `/assets/js/script.js` 中的相关代码删除，同理，如果不需要代码高亮也可在这个文件中将相关代码删除。

### 修改许可协议

在 `post.hbs` 文件的分享链接部分声明博客内容所使用的许可协议，默认使用 [Attribution-NonCommercial-ShareAlike 3.0 Unported](http://creativecommons.org/licenses/by-nc-sa/3.0/)。

### Disqus 评论

Disqus 评论加载比较慢，所以使用了 lazy-load 的方式，在 `/assets/js/script.js` 的最下方找到 Disqus 相关代码，将 `window.disqus_shortname` 的值修改为自己的 shortname 。每篇文章的发表时间（`{{date format='YYYYMMDD'}}`）作为 identifier。

### 调整配色

个人非常不擅长配色，所以在 `/assets/_sass/style.scss` 文件中尽可能多地定义了颜色变量方便大家修改配色。关于默认的主题配色也请大家多提建议。

### 支持 Ghost 插件

如果需要使用 Ghost 插件，可能需要在 `<head>` 与 `<body>` 内添加以下两个标签 `{{ghost_head}}` 与 `{{ghost_foot}}` （与 Wordpress 类似）。

### Pjax 与 Google analytics

如果需要配置 Google analytics 请查看：http://stackoverflow.com/questions/9527965/jquery-pjax-and-google-analytics

## 已知问题

1. IE9 及以下浏览器访问时会自动跳转到 `/ie.html` 提示不支持当前浏览器，因为 Ghost 还不支持静态页面，所以会返回 404 错误。

2. Ghost 输出文章标题时会将标题内容作 ID 可当定位锚用，但是当标题全部是中文时输出为空，导致了右侧的 TOC 链接无效。如果中英文混合标题中的英文完全相同也会输出重复的 ID 导致定位锚跳不准确。Ghost 将会在 0.5 版本中改善这个问题，详见 [https://github.com/TryGhost/Ghost/issues/1602](https://github.com/TryGhost/Ghost/issues/1602)。想到一个 workaround，给每个标题重新生成一串随机字母做 ID，但这样可能会影响分享链接，默认关闭，可以在 `/assets/js/script.js` 中启用。

3. 键盘 <kbd>Space</kbd> <kbd>PgUp</kbd> <kbd>PgDn</kbd> <kbd>↑</kbd> <kbd>↓</kbd> 等快捷键无效，这是由于当前的布局方式影响的。iOS7 Mobile Safari 自动隐藏地址栏也会无效。


## Credits

* [jquery-pjax](https://github.com/defunkt/jquery-pjax)
* [NProgress.js](http://ricostacruz.com/nprogress/)
* [Prism.js](http://prismjs.com)

## Copyright & License

Copyright (c) 2013 Peiwen Lu - Released under The MIT License.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.