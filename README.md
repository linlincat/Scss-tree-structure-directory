##有关SCSS结构目录的总结【本文作者：法国Hugo Giraudel，来至网络资源】
---
###理想情况下，目录层次如下所示：

```
    sass/
        |
        |– base/
        |   |– _reset.scss       # Reset/normalize
        |   |– _typography.scss  # Typography rules
        |   ...                  # Etc…
        |
        |– components/
        |   |– _buttons.scss     # Buttons
        |   |– _carousel.scss    # Carousel
        |   |– _cover.scss       # Cover
        |   |– _dropdown.scss    # Dropdown
        |   ...                  # Etc…
        |
        |– layout/
        |   |– _navigation.scss  # Navigation
        |   |– _grid.scss        # Grid system
        |   |– _header.scss      # Header
        |   |– _footer.scss      # Footer
        |   |– _sidebar.scss     # Sidebar
        |   |– _forms.scss       # Forms
        |   ...                  # Etc…
        |
        |– pages/
        |   |– _home.scss        # Home specific styles
        |   |– _contact.scss     # Contact specific styles
        |   ...                  # Etc…
        |
        |– themes/
        |   |– _theme.scss       # Default theme
        |   |– _admin.scss       # Admin theme
        |   ...                  # Etc…
        |
        |– utils/
        |   |– _variables.scss   # Sass Variables
        |   |– _functions.scss   # Sass Functions
        |   |– _mixins.scss      # Sass Mixins
        |   |– _helpers.scss     # Class & placeholders helpers
        |
        |– vendors/
        |   |– _bootstrap.scss   # Bootstrap
        |   |– _jquery-ui.scss   # jQuery UI
        |   ...                  # Etc…
        |
        |
        `– main.scss             # primary Sass file
```
##Base文件夹
base/文件夹存放项目中的模板文件。在这里，可以找到重置文件、排版规范文件或者一个样式表（我通常命名为_base.scss）——定义一些HTML元素公认的标准样式。

    * _base.scss
    * _reset.scss
    * _typography.scss

##Layout文件夹
layout/文件夹存放构建网站或者应用程序使用到的布局部分。该文件夹存放网站主体（头部、尾部、导航栏、侧边栏...）的样式表、栅格系统甚至是所有表单的CSS样式。  

    * _grid.scss
    * _header.scss
    * _footer.scss
    * _sidebar.scss
    * _forms.scss
    * _navigation.scss

> NOTE --- layout/文件夹也会被称为partials/,>具体使用情况取决于个人喜好。

##Components文件夹

对于小型组件来说，有一个components/文件夹来存放。相对于layout/的宏观（定义全局线框结构），components/更专注于局部组件。该文件夹包含各类具体模块，基本上是所有的独立模块，比如一个滑块、一个加载块、一个部件……由于整个网站或应用程序主要由微型模块构成，components/中往往有大量文件。

    * _media.scss
    * _carousel.scss
    * _thumbnails.scss

>NOTE --- components/文件夹也会被称为modules/, 具体使用情况取决于个人喜好。

##Pages文件夹

如果页面有特定的样式，最好将该样式文件放进pages/文件夹并用页面名字。例如，主页通常具有独特的样式，因此可以在pages/下包含一个_home.scss以实现需求。

    * _home.scss
    * _contact.scss

##Themes文件夹

在大型网站和应用程序中，往往有多种主题。虽有多种方式管理这些主题，但是我个人更喜欢把它们存放在themes/文件夹中。

    * _theme.scss
    * _admin.scss

##Utils文件夹

utils/文件夹包含了整个项目中使用到的Sass辅助工具，这里存放着每一个全局变量、函数、混合宏和占位符。  该文件夹的经验法则是，编译后这里不应该输出任何CSS，单纯的只是一些Sass辅助工具。

    * _variables.scss
    * _mixins.scss
    * _functions.scss
    * _placeholders.scss(frequently named_helpers.scss)

>NOTE --- 该文件夹的经验法则是，编译后这里不应该输出任何CSS，单纯的只是一些Sass辅助工具。

##Vendors文件夹
最后但并非最终的是，大多数的项目都有一个vendors/文件夹，用来存放所有外部库和框架（Normalize, Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered……）的CSS文件。将这些文件放在同一个文件中是一个很好的说明方式:"嘿，这些不是我的代码，无关我的责任。"

    * _normalize.scss
    * _bootstrap.scss
    * _jquery-ui.scss
    * _select2.scss


如果你重写了任何库或框架的部分，建议设置第8个文件夹vendors-extensions/来存放，并使用相同的名字命名。  

例如，vendors-extensions/_boostrap.scss文件存放所有重写Bootstrap默认CSS之后的CSS规则。这是为了避免在原库或者框架文件中进行二次编辑——显然不是好方法。


##Main文件

主文件（通常写作main.scss）应该是整个代码库中唯一开头不用下划线命名的Sass文件。除 @import和注释外，该文件不应该包含任何其他代码。

文件应该按照存在的位置顺序依次被引用进来：


```
1. vendors/
2. utils/
3. base/
4. layout/
5. components/
6. pages/
7. themes/
```

##为了保持可读性，主文件应遵守如下准则：

* 每个 @import引用一个文件；
* 每个 @import单独一行；
* 从相同文件夹中引入的文件之间不用空行；
* 从不同文件夹中引入的文件之间用空行分隔；
* 忽略文件扩展名和下划线前缀。



```java
@import 'vendors/bootstrap';
@import 'vendors/jquery-ui';

@import 'utils/variables';
@import 'utils/functions';
@import 'utils/mixins';
@import 'utils/placeholders';

@import 'base/reset';
@import 'base/typography';

@import 'layout/navigation';
@import 'layout/grid';
@import 'layout/header';
@import 'layout/footer';
@import 'layout/sidebar';
@import 'layout/forms';

@import 'components/buttons';
@import 'components/carousel';
@import 'components/cover';
@import 'components/dropdown';

@import 'pages/home';
@import 'pages/contact';

@import 'themes/theme';
@import 'themes/admin';
```

这里还有另一种引入的有效方式。令人高兴的是，它使文件更具有可读性；令人沮丧的是，更新时会有些麻烦。不管怎么说，由你决定哪一个最好，这没有任何问题。 对于这种方式，主要文件应遵守如下准则：

* 每个文件夹只使用一个@import
* 每个@import之后都断行
* 每个文件占一行
* 新的文件跟在最后的文件夹后面
* 文件扩展名都可以省略


```java

@import
  'vendors/bootstrap',
  'vendors/jquery-ui';

@import
  'utils/variables',
  'utils/functions',
  'utils/mixins',
  'utils/placeholders';

@import
  'base/reset',
  'base/typography';

@import
  'layout/navigation',
  'layout/grid',
  'layout/header',
  'layout/footer',
  'layout/sidebar',
  'layout/forms';

@import
  'components/buttons',
  'components/carousel',
  'components/cover',
  'components/dropdown';

@import
  'pages/home',
  'pages/contact';

@import
  'themes/theme',
  'themes/admin';
```

>NOTE --- 为了不用亲自引入每一个文件，有一个叫做sass-globbing的Ruby Sass扩展程序，使在Sass的@import中,使其做为glob模式，就像这样：@import "components/*"  

>话虽如此，却不推荐它，因为它按照字母顺序引入文件，这往往并不是想要的，特别是处理一个对源文件顺序有所依赖的编程语言的时候。


##Shame文件
另一个有意思的方面，由业内已流行的Harry Roberts, Dave Rupert 和 Chris Coyier引起的，那就是将所有的CSS声明、Hack行为和我们不支持的行为放入一个shame file。该文件命名为 _shame.scss，在所有文件之后被引用，放在所有样式表的最后。

```java
/**
 * Nav specificity fix.
 *
 * Someone used an ID in the header code (`#header a {}`) which trumps the
 * nav selectors (`.site-nav a {}`). Use !important to override it until I
 * have time to refactor the header stuff.
 */
.site-nav a {
    color: #BADA55 !important;
}
```