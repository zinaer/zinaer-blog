---
layout: post
title:  "抛弃陈旧的观念，拥抱新时代的 PHP"
date:   2017-10-28 06:12:10 +0800
---
根据 PHP 官方的消息，最近，PHP 开发者团队发布了 PHP 7.0.25，修复了一些安全问题。自从 PHP 7 的发布，给 PHP 带来了很大性能的提升，也进一步加速了现代 PHP 的重生。相信有很多人还秉持着传统的旧观念在看待和使用 PHP，今天我们来聊一聊新时代的 PHP。

### 什么是 PHP

PHP（全称：PHP：Hypertext Preprocessor，即 “PHP：超文本预处理器”）是一种开源的通用计算机脚本语言，尤其适用于网络开发并可嵌入 HTML 中使用。PHP 的语法借鉴吸收 C 语言、Java 和 Perl 等流行计算机语言的特点，易于一般程序员学习。PHP 的主要目标是允许网络开发人员快速编写动态页面，但 PHP 也被用于其他很多领域。

### PHP 的历史

PHP 诞生于 90 年代互联网的兴起，常和 Apache 或 Nginx 等 Web 服务器一起，提供动态的内容服务。不过 PHP 也可以像 Bash、Python 一样构建强大的命令行工具。这个特性有不少人不知道。

1995 年，丹麦程序员**拉斯姆斯·勒多夫**为了维护他的个人网页，用 C 语言开发了 PHP。1997 年，以色列程序员 **Zeev Suraski** 和 **Andi Gutmans**，重写了 PHP 的解释引擎，最后发布了 PHP 3，从此，开始了 PHP 核心的改写，并在 1999 年成立了 Zend Technologies 来管理 PHP 的开发。2000 年，发布了 PHP 4。2004 年，发布了 PHP 5，包含了许多新特性，像强化的物件导向功能、引入 PDO，以及许多性能上的增强。

2015 年，PHP 7 发布，主要改进有 PHPNG、JIT 引擎、抽象语法树编译、异步编程。PHPNG 项目是国内鸟哥发起的 PHP 引擎重构项目，取得了很大的成就，也促成了 PHP 7 的发布。

### 新时代的 PHP

现在，PHP 语言发展迅速，由来自全球的几十名核心开发者提供支持。依托于一大批优秀的工具，也使开发和部署变得更容易，更便捷。

版本控制软件（如：Git）能帮助我们维护一个可审查的代码历史，可以创建代码分支，fork 代码和合并代码。虚拟化工具（如：Vagrant）以及配置工具（如：Ansible、Chef 和 Puppet）使我们可以搭建和生产服务器一致的本地开发环境。轻量级的虚拟化解决方案 Docker 使我们可以在一台机器创建不同运行环境，来运行多个网站。依赖管理工具 Composer 方便用来使用专门的 PHP 组件。我们的代码遵循 PSR（代码风格标准），方便使用别人的代码，或者被别人使用。PHPUnit 等工具彻底测试我们的代码。将应用放在 Nginx 这样的 Web 服务器，使用 PHP 的 FastCGI 进程管理应用，而且使使用 Opcode 缓存和对象缓存来提升应用的性能。

现代的 PHP 有许多令人兴奋的新特性，使得 PHP 越来越好。

#### 命名空间

这是个非常重要的特性，命名空间在 PHP 5.3.0 引入，其作用是按照一种虚拟层次结构组织 PHP 代码，这种层次结构类似操作系统中文件系统的目录结构。现代的 PHP 组件和框架都放在各自全局唯一的厂商命名空间中，以免与其他厂商使用的常见类名冲突。

**声明命名空间**

每个 PHP 类、接口、函数和常量都在命名空间里。命名空间在 PHP 文件 `<?` 之后第一行声明，以 `namespace` 开头。

```php
<?php
namespase Zinaer;
```

命名空间，顶层建议设置厂商的名字，不容易重复，比如上边厂商名称是 `Zinaer`。在它下面设置的 PHP 类、接口、函数和变量都和它有关系。

子命名空间的声明和上边的类似，需要注意的是使用 `\` 将命名空间和子命名空间分开。

```php
<?php
namespace Zinaer\Http
```

在同一个命名空间或子命名空间中的所有类没必要在同一个 PHP 文件中声明，只要在 PHP 文件顶部指定命名空间或子命名空间，这个文件中的所有代码就是这个命名空间的一部分。所以可以在不同文件编写同一个命名空间的多个类。

**导入和别名**

导入是指，如果在 PHP 文件中想使用哪个命名空间、类、接口、函数和常量，只需要导入就可以了。

别名是为了使用简单的名称引用导入的类、接口、函数或变量。

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller
{
    /**
     * 储存一个新用户。
     *
     * @param  Request  $request
     * @return Response
     */
    public function store(Request $request)
    {
        $name = $request->input('name');

        //
    }
}
```

使用 `use` 导入了 `Illuminate\Http\Request`，从而后面的代码可以直接使用 `Request`，不用每次调用都使用完整的 `Illuminate\Http\Request`。

如果你足够懒，还可以使用别名。

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request as Res;
```

后面的代码就可以使用 `Res` 代替 `Request`。

还可以导入函数（use func）或常量（use constant），比如：

```php
<?php
use func Namespace\functionName;

functionName();

```

```php
use contant Namespace\CONST_NAME;

echo CONST_NAME;
```

他们同样支持别名，和类别名使用方式一样。

**全局命名空间**

有些代码可能没有命名空间，这些代码在全局命名空间中。需要在类、接口、函数或常量的名称前加 `\` 符号进行使用。

```php
<?php
namespace Zinaer\App;

class User
{
	public function login()
	{
		throw new \Exception();
	}
}
```

**自动加载**

命名空间奠定了 PSR-4 自动加载标准，大多数现代 PHP 组件都使用了自动加载模式，使用依赖管理器 Composer 可以自动项目的依赖。

#### 使用接口

学会使用接口，可以容易的把第三方 PHP 组件集成到自己的应用中。我们不关心第三方代码是怎么实现接口的，只关心第三方代码是否实现了指定接口。

在上文介绍的 `use Illuminate\Http\Request;` 就是导入了 `Request` 接口。这个接口定义了，获取请求路径、获取请求的 URL、获取请求方法等功能。

#### Trait (代码复用)

Trait 是 PHP 5.4.0 引入的新概念，既像类，又像接口，其实都不是。Trait 有两个作用，表明类可以做什么，提供模块化的实现。

**为什么使用 Trait**

PHP 语言使用一种典型的继承模型。在这个模型中，我们先编写一个通用的父类，实现基本功能，然后再集成它实现具体的类，这叫继承层次结构。但是，如果是两个无关的 PHP 类，具有某些类似的行为，应该怎么做？

第一种方法：写个父类，让两个子类继承他，这种方法，强制让两个无关的类，继承一个祖先，破坏了继承层次。第二种方法：创建一个接口，定义需要哪些接口，然后在两个类中都实现这个接口。这种虽然保留了继承结构，但是需要重复实现相同的功能。不符合 DRY 原则。

这时候就产生了 Trait，Trait 能把模块化的实现方式注入多个无关的类中。

**如何创建 Trait**

```php
trait MyTrait {
	// 这里是实现
}
```

像定义类和接口一样，一个文件定义一个 Trait 是个良好的习惯。Trait 只需要定义属性和方法，其余什么都不用做。

**如何使用 Trait**

```php
class MyClass
{
	use MyTrait;
}
```

#### 生成器

PHP 生成器是 PHP 5.5.0 引入的功能。生成器就是简单的迭代器。这是个很有用的功能，但往往没有被利用起来。

标准 PHP 迭代器经常在内存中执行迭代操作，这要预先计算出数据集，更不要说用特定方式计算大量数据，性能影响严重。此时可以使用生成器，即时计算并产出后续值，不占用宝贵的内存资源。

**创建生成器**

生成器是 PHP 函数，需要在函数中一次或多次使用 `yield` 关键字。与普通 PHP 函数不同的是，从不返回值，只产出值。

```php
<?php
function myGenerator() {
	yield 'value1';
	yield 'value2';
	yield 'value3';
}
```

调用 PHP 生成器函数时，PHP 会返回一个属于 Generator 类的对象，这个对象可以使用 foreach() 函数迭代。每次迭代，PHP 会要求 Generator 实例计算并提供下一个迭代的值。生成器的优雅体现在，每次产出一个值后，生成器内部状态都会停顿，请求下一个值时，内部状态又会恢复。直到函数结束，或者空的 return; 语句。

```php
<?php
foreach (myGeneratro() as $value) {
	echo $value, PHP_EOL;
}
``` 

#### 闭包

闭包是指在创建时封装周围状态的函数，即便包含闭包的环境不存在了，闭包中封装的状态还存在。匿名函数是没有名称的函数，匿名函数可以赋值给变量，也能像其他对象一样传递。同样支持调用和传参。理论上，闭包和匿名函数是不同的概念，但在 PHP 中是一样的。

闭包和匿名函数是伪装成函数的对象，虽然语法和普通函数一样。

```php
<?php
$closure = function ($name) {
	return sprintf('Hello %s', $name);
}

echo $closure('Zinaer');
// Hello Zinaer
```

`$closure` 变量就是一个闭包。

通常把闭包当做函数和方法的回调使用，这样写出的代码更简洁，更清晰。

```php
<?php
$numberPlusOne = array_map(function ($number) {
	return $number + 1;
}, [1, 2, 3]);
print_r($numberPlusOne);
// [2, 3, 4]
```

**附加状态**

常使用 bindto() 方法或 `use` 关键字，为 PHP 闭包附加状态。

```php
<?php
function enclosePerson($name) {
	return function ($doCommand) use ($name) {
		return sprintf('%s, %s', $name, $doCommand);
	}
}
// 封装 `Zinaer` 到闭包
$zinaer = enclosePerson('Zinaer');

// 传参，调用闭包
echo $zinaer('it is good!');
// Zinaer, it is good!
```

#### Zend OPcache
 
从 PHP 5.5.0 开始，PHP 内置了 Zend OPcache（字节码缓存），默认没有开启，需要主动开启。

为什么需要字节码缓存？

PHP 是解释型语言，PHP 解析器执行 PHP 脚本时会解析 PHP 脚本代码，把 PHP 编译成一系列 Zend 操作码，然后执行字节码。每次请求都是这样，会消耗很多资源。字节码缓存能预先存储编译好的 PHP 字节码，这样，执行 PHP 脚本时，PHP 解释器不用每次都读取、解析和编译 PHP 代码。从内存中读取预先编译好的字节码，然后立即执行，不但节省时间，同时也提高了应用的性能。

#### 内置的 HTTP 服务器

从 PHP 5.4.0 起，PHP 内置了 Web 服务器。在不安装 Nginx 等 Web 服务器的情况下，这个服务器可以实现在本地编写代码和预览。

```bash
php -S localhost:4000
```

上述命令会启动一个 PHP Web 服务器。如果需要局域网中其它机器访问可以使用 `0.0.0.0` 代替 `localhost`。

**查看使用的是否是内置服务器**

```php
<?php
if (php_sapi_name() === 'cli-server') {
	// PHP 内置的 Web 服务器
}
else {
	// 其它服务器
}
```

PHP 内置服务器不能用于生产环境，只能在本地开发环境中使用。

#### 标准

PHP 组件和框架有很多，但是旧的框架是单独开发的，不能与其它框架共享代码。多位 PHP 框架的开发者意识到了这个问题，并成立了 PHP-FIG 进行规范的制定，目的是实现框架的互操作性，比如：通过接口、自动加载机制和标准的风格，让框架相互合作。

PSR 是 PHP-FIG 制定定的规范，目前已经表决通过了 6 套标准，并得到大部分 PHP 框架的支持和认可。其中包括：

1. 基础编码规范
2. 编码风格规范
3. 日志接口规范
4. 自动加载规范
6. 缓存接口规范
7. HTTP 消息接口规范

为什么没有 5 ？不是笔者写错了，是因为 5 PHPDoc 还在起草中。

#### 组件

现代 PHP 应该较少使用庞大的框架，而是应该更多的使用具有互操作性的专门组件制定解决方案。其他开发者已经用了无数时间创建、优化和测试专门的组件，以便让组件尽量做好一件事。如果想快速开发更好的应用，不是使用这些组件，而是自己重新造轮子，是非常不明智的。

那么如何挑选组件？

好的组件应该具有作用单一、小型、合作、测试良好、文档完善的特征。我们可以在 [Packagist](https://packagist.org) 中查找符合这些特征的组件，然后用 Composer 来安装管理这些组件。

#### 测试

测试是开发 PHP 过程中的重要一步，但往往被忽视了。测试应该贯穿于开发应用的开始、过程中和结束后。

为什么测试？

很简单，通过测试可以确保 PHP 应用始终按照我们预期的方式运行。

测试是什么？

我们应该测试应用的最小部分，比如 PHP 应用由类、方法和函数组成。所以应该隔离测试他们，确保表现符合预期，这样组合在一起才能确保整个应用能正常运行，这种测试叫单元测试。

为了进一步确保应用没问题，还要使用自动化测试工具来验证应用的整体行为，这种测试叫功能测试。

可以使用 PHPUnit 编写和运行测试，使用 Travis CI 进行自动化测试。

### 结束语

上边简单介绍了新时代 PHP 的一些特性、组件、测试等，是否对新时代 PHP 有了新的认识 ？希望大家可以抛弃陈旧的观念，拥抱新时代的 PHP，这不会令你失望！

====

![](http://pic.zinaer.com/201710/zanshang.jpg)

<small>*微信扫一扫进行赞赏*</small>

![](http://pic.zinaer.com/201710/zinaer_wx.jpg)

<small>*微信扫一扫关注此公众号*</small>






