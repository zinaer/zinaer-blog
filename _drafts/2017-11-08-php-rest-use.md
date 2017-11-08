---
layout: post
title:  "玩转 PHP 系列：使用 RESTful API"
date:   2017-11-09 06:35:12 +0800
---

REST 是一类简单的 Web API，可以利用 REST 使用 HTTP 方法（如：GET 和 POST）向 URL 做出请求。URL 和体（通常采用 JSON 或 XML 格式）描述了你想要管理的资源，方法则告诉服务器要采取什么动作。

GET 告诉服务器你希望获取现有的数据，POST 表示你想要增加一个新资源，PUT 可以替换一个资源，或者创建一个命名资源，DELETE 就是要删除资源。

REST 的妙处在于使用了现有的标准。由于大多数开发人员都熟悉 HTTP 和 JSON，REST 的学习曲线很短而且很浅。

REST 也有缺点：对于传入或者返回的数据没有一个标准模式。每个网站都可以使用自己认为合适的模式。对于小型服务来说这不是问题，不过如是设计不合理，随着服务的增长，这就会带来复杂性。

可以采用多种不同方法用 PHP获取远程 URL。这里我们介绍三种方法：标准文件函数、cURL 扩展和 PEAR 的 HTTP_Request2 类。利用这三种方法通常能完成你需要的所有工作。

使用标准文件函数（如 file_get_contents()） 很简单，也很方便。它会自动追随重定向。它对 HTTP 和 FTP 都适用。缺点是它要求打开 allow_url_fopen 配置指令。

cURL 扩展非常强大，就像一个 “万金油” 。它依赖流行的 libcurl 提供一个快速、可配置的机制，来处理各种不同的网络请求。如果你的服务器上可以使用这个扩展，建议务必采用这种方法。

如果上述两种方法不可用，PEAR HTTP_Request2 模块可以提供帮助。与所有 PEAR 模块类似，这也是纯 PHP 模块，所有如果可以在服务器上保存 PHP 文件，就可以用这个方法。请求一个远程 URL，你想做的所有工作 HTTP_Request2 几乎都能支持，包括修改请求首部和体、使用任意的方法，以及获取响应首部。

### 用 GET 方法获取 URL

希望获取一个 URL 的内容。

```php
// 方法一：file_get_contents
$page = file_get_contents('https://www.zinaer.com');

// 方法二：cURL
$ch = curl_init('https://www.zinaer.com');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$page = curl_exec($ch);
curl_close($ch);

// 方法三：HTTP_Request2
require_once 'HTTP/Request2.php';
$res = new HTTP_Request2('https://www.zinaer.com');
$page = $res->send()->getBody();
```

与所有 PHP 文件处理函数一样，file_get_contents() 使用了 PHP 的流特性。这说明，它不仅可以处理本地文件，还可处理各种网络资源，包括 HTTP URL。

要获取一个包含查询字符串变量的页面，可以使用 http_build_query() 创建这个查询字符串：

```php
$vars = array('page' => 4, 'search' => 'video');
$qs = http_build_query($vars);
$url = 'https://www.zinaer.com/search.php?' . $qs;
$page = file_get_contents($url);
```

要获取需要账号和密码登录的 URL：

```php
// 方法一
$url = 'http://zinaer:abcd1234@www.zinaer.com/secrets.php';
$page = file_get_contents($url);

// 方法二
$ch = curl_init('http://www.zinaer.com/secrets.php');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_USERPWD, 'zinaer:abcd1234');
$page = curl_exec($ch);
curl_close($ch);

// 方法三
require_once 'HTTP/Request2.php';

$res = new HTTP_Request2('https://www.zinaer.com/secrets.php');
$res->setAuth('zinaer', 'abcd1234', HTTP_Request2::AUTH_DIGEST);
$page = $res->send()->getBody();
```

file_get_contents() 和 fopen() 函数支持一个流上下文参数，允许指定获取流的有关选项。其中一个选项是 max_redirects, 重定向的最大数目。

```php

```




