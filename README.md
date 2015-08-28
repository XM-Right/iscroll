<h1 id="intro">iscroll，为网络平滑滚动</h1>

<h1 id="intro">iScroll, smooth scrolling for the web</h1>

iScroll 是高性能，体积小，无依赖性，多平台的 javaScript 滚轮。

iScroll is a high performance, small footprint, dependency free, multi-platform javascript scroller.

它适用于台式机、手机和智能电视

It works on desktop, mobile and smart TV. It has been vigorously optimized for performance and size so to offer the smoothest result on modern and old devices alike.

iScroll 不只是 `scroll`， 它可以处理任何与用户交互的移动元素，它增加了滚动、缩放、平移、无限滚动、视差滚动、旋转木马到你的项目，并设法做到大小仅4kb，给它一把扫帚，它也会清理你的办公室。

iScroll does not just *scroll*. It can handle any element that needs to be moved with user interaction. It adds scrolling, zooming, panning, infinite scrolling, parallax scrolling, carousels to your projects and manages to do that in just 4kb. Give it a broom and it will also clean up your office.

即使在平台上，其中原生的滚动是不够好，iScroll添加功能，将是不可能的，否则。具体做法是：

Even on platforms where native scrolling is good enough, iScroll adds features that wouldn't be possible otherwise. Specifically:

* 
* 自定义动画
* 自定义事件
* 出包支持多平台，从旧的 Android 到最新的iPhone，从浏览器到互联网浏览器。

* Granular control over the scroll position, even during momentum. You can always get and set the x,y coordinates of the scroller.
* Animation can be customized with user defined easing functions (bounce, elastic, back, ...).
* You can easily hook to a plethora of custom events (onBeforeScrollStart, onScrollStart, onScroll, onScrollEnd, flick, ...).
* Out of the box multi-platform support. From older Android devices to the latest iPhone, from Chrome to Internet Explorer.

<h2 id="iscroll-versions">The many faces of iScroll</h2>

iScroll 关于所有的优化。为了达到最高的性能，已经被分成多个版本，你可以根据你的需求挑选你需要的版本。

iScroll is all about optimization. To reach the highest performance it has been divided into multiple versions. You can pick the version that better suits your need.

目前我们有以下的香水：

Currently we have the following fragrances:

* **iscroll.js**，它是通用的脚本，它包括最常用的功能和非常高性能的一个小足迹。
* **iscroll-lite.js**，它是一个精简版的主脚本。它不支持卡、滚动条、鼠标滚轮、按键绑定。但如果你需要的是滚动（尤其是在移动端） *iScroll lite* 是最小、最快的解决方案。
* **iscroll-probe.js**，探测当前滚动的位置是一个艰巨的任务，这就是我为什么决定建立一个专门的版本。如果你需要知道在一个特定的时间滚动位置，这个 iScroll 适合你。（我在做一些测试，这个可能最终在常规的 `iScroll.js` 脚本里，所以密切观察就可以了）。
* **iscroll-zoom.js**， 增加了缩放到标准的滚动。
* **iscroll-infinite.js**， 能够做到无限缓存滚动。在移动设备中处理很长的列表元素是不容易的任务。 *iScroll infinite* 使用缓存机制，可以让你滚动无限数量潜在的元素。

* **iscroll.js**, it is the general purpose script. It includes the most commonly used features and grants very high performance in a small footprint.
* **iscroll-lite.js**, it is a stripped down version of the main script. It doesn't support snap, scrollbars, mouse wheel, key bindings. But if all you need is scrolling (especially on mobile) *iScroll lite* is the smallest, fastest solution.
* **iscroll-probe.js**, probing the current scroll position is a demanding task, that's why I decided to build a dedicated version for it. If you need to know the scrolling position at any given time, this is the iScroll for you. (I'm making some more tests, this might end up in the regular `iscroll.js` script, so keep an eye on it).
* **iscroll-zoom.js**, adds zooming to the standard scroll.
* **iscroll-infinite.js**, can do infinite and cached scrolling. Handling very long lists of elements is no easy task for mobile devices. *iScroll infinite* uses a caching mechanism that lets you scroll a potentially infinite number of elements.

<h2 id="getting-started">Getting started</h2>

所以你要变成一个 iSroll 大师， 因为我会让你变成。

So you want to be an iScroll master. Cool, because that is what I'll make you into.

学习 iScroll 最好的方式是通过查看演示。在文档中你会发现一个 `demo` 文件夹[stuffed with examples](https://github.com/cubiq/iscroll/tree/master/demos)。这里有大部分的脚本功能概述。

The best way to learn the iScroll is by looking at the demos. In the archive you'll find a `demo` folder [stuffed with examples](https://github.com/cubiq/iscroll/tree/master/demos). Most of the script features are outlined there.

`iScroll` 是一个类，需要启动每个滚动区域。………………………………

`IScroll` is a class that needs to be initiated for each scrolling area. There's no limit to the number of iScrolls you can have in each page if not that imposed by the device CPU/Memory.

尽量保持简单的 DOM 结构。 …………

Try to keep the DOM as simple as possible. iScroll uses the hardware compositing layer but there's a limit to the elements the hardware can handle.

最佳的 HTML 结构：

The optimal HTML structure is:

    <div id="wrapper">
        <ul>
            <li>...</li>
            <li>...</li>
            ...
        </ul>
    </div>

iScroll 必须应用到滚动区域的包装器内。在上面的例子中 `UL` 将滚动。只有容器的第一个子元素能够滚动，另外的子元素将被简单忽略。

iScroll must be applied to the wrapper of the scrolling area. In the above example the `UL` element will be scrolled. Only the first child of the container element is scrolled, additional children are simply ignored.

`box-shadow`、`opacity`、`text-shadow` 和 `alpha` 通道是所有属性不与硬件加速去很好的结合在一起。滚动可能会好看一些因素，但只要你的DOM变得更加复杂，你就会开始遇到滞后和跳跃。

<div class="tip">
<p><code>box-shadow</code>, <code>opacity</code>, <code>text-shadow</code> and alpha channels are all properties that don't go very well together with hardware acceleration. Scrolling might look good with few elements but as soon as your DOM becomes more complex you'll start experiencing lag and jerkiness.</p>

有时一个背景图片来模拟阴影的性能比 `box-shadow` 要好，底线是：实验的CSS属性，你会出现一个小的CSS的变化可以做到性能上的差异感到惊讶

<p>Sometimes a background image to simulate the shadow performs better than <code>box-shadow</code>. The bottom line is: experiment with CSS properties, you'll be surprised by the difference in performance a small CSS change can do.</p>
</div>

最小的回调启动脚本如下：

The minimal call to initiate the script is as follow:

    <script type="text/javascript">
    var myScroll = new IScroll('#wrapper');
    </script>

第一个参数可以表示是该滚动容器元素的 DOM 选择器或者一个参考元素本身的字符串，下面是一个有效的语法：

The first parameter can be a string representing the DOM selector of the scroll container element OR a reference to the element itself. The following is a valid syntax too:

    var wrapper = document.getElementById('wrapper');
    var myScroll = new IScroll(wrapper);

所以基本上要么你直接传递元素或使用在 `querySelector` 的字符串。因此选择一个包装它的类名，而不是 ID ,你会怎么做：

So basically either you pass the element directly or a string that will be given to `querySelector`. Consequently to select a wrapper by its class name instead of the ID, you'd do:

    var myScroll = new IScroll('.wrapper');

需要注意的是 iScroll 使用 `querySelector` 而不是用 `querySelectorAll`， 所以只有选择第一个出现的才是。如果你需要 iScroll 应用于多个多个对象，你可以自己建立时间周期。

Note that iScroll uses `querySelector` not `querySelectorAll`, so only the first occurrence of the selector is used. If you need to apply iScroll to multiple objects you'll have to build your own cycle.

你不需要严格将实例分配给一个变量 `myScroll` ，但是它是方便随时参照 iScroll。

<div class="tip">
<p>You don't strictly need to assign the instance to a variable (<code>myScroll</code>), but it is handy to keep a reference to the iScroll.</p>

例如你稍后可以检查 <a href="#scroller-info">scroller position</a> or <a href="#destroy">unload unnecessary events</a>，当你不再需要 iScroll。

<p>For example you could later check the <a href="#scroller-info">scroller position</a> or <a href="#destroy">unload unnecessary events</a> when you don't need the iScroll anymore.</p>
</div>

<h2 id="initialization">Initialization</h2>

该 iScroll 需要在 DOM 准备启动，最安全的方法是开始在 window 的 `onload` 事件，`DOMConrentLoaded` 或者内联初始化也可以，但是记住脚本需要知道滚动区域的高度/宽度。如果你有图像没有明确的高度/宽度声明，iScroll将有可能结束一个错误的滚动条的大小。

The iScroll needs to be initiated when the DOM is ready. The safest bet is to start it on window `onload` event. `DOMContentLoaded` or inline initialization are also fine but remember that the script needs to know the height/width of the scrolling area. If you have images that don't have explicit width/height declaration, iScroll will most likely end up with a wrong scroller size.

添加 `opsition:relative` 或者 `absolute` 到这个滚动容器（ the wrapper )。这本身通常会解决大部分的问题，错误的计算包装尺寸。

<div class="important">
<p>Add <code>position:relative</code> or <code>absolute</code> to the scroll container (the wrapper). That alone usually solves most of the problems with wrongly calculated wrapper dimensions.</p>
</div>

综上所述，最小的 iScroll 配置是：

To sum up, the smallest iScroll configuration is:

    <head>
    ...
    <script type="text/javascript" src="iscroll.js"></script>
    <script type="text/javascript">
    var myScroll;
    function loaded() {
        myScroll = new IScroll('#wrapper');
    }
    </script>
    </head>
    ...
    <body onload="loaded()">
    <div id="wrapper">
        <ul>
            <li>...</li>
            <li>...</li>
            ...
        </ul>
    </div>
    </body>

参考 [barebone example](http://lab.cubiq.org/iscroll5/demos/barebone/) 中最少的 CSS/HTML 要求更多的细节。

Refer to the [barebone example](http://lab.cubiq.org/iscroll5/demos/barebone/) for more details on the minimal CSS/HTML requirements.

如果你有一个复杂的 DOM 节点，有时聪明添加 `onload` 事件一点延迟 iScroll 的初始化。执行 iScroll 用100 或者 200毫秒的延迟给浏览器，稍微休息一下，可以节省你执行 iScroll。

<div class="tip">
<p>If you have a complex DOM it is sometimes smart to add a little delay from the <code>onload</code> event to iScroll initialization. Executing the iScroll with a 100 or 200 milliseconds delay gives the browser that little rest that can save your ass.</p>
</div>

<h2 id="configuring">Configuring the iScroll</h2>

iScroll 可以通过在初始化阶段将第二个参数来配置。

iScroll can be configured by passing a second parameter during the initialization phase.

    var myScroll = new IScroll('#wrapper', {
        mouseWheel: true,
        scrollbars: true
    });

上面的例子打开鼠标滚轮支持和滚动条。

The example above turns on mouse wheel support and scrollbars.

初始化完成以后，你可以从选项对象访问标准化值。例如：

After initialization you can access the *normalized* values from the `options` object. Eg:

    console.dir(myScroll.options);

以上将返回配置 `myScroo` 实例中运行。通过 *normalized* 我的意思是如果你设置 `useTransform:true` （ 例如 ）但是浏览器不支持 CSS transfors， `useTransfor` 将会是 `false`。

The above will return the configuration the `myScroll` instance will run on. By *normalized* I mean that if you set `useTransform:true` (for example) but the browser doesn't support CSS transforms, `useTransform` will be `false`.

<h2 id="the-core">Understanding the core</h2>

iScroll 使用各种技术基于 设备/浏览器 功能来滚动。**通常你不需要配置引擎**， iScroll 足够聪明，挑选最适合你的。

iScroll uses various techniques to scroll based on device/browser capability. **Normally you don't need to configure the engine**, iScroll is smart enough to pick the best for you.

但是了解 iScroll 这些工作机制和如何配置是非常重要的。

Nonetheless it is important to understand which mechanisms iScroll works on and how to configure them.

### <small>options.</small>useTransform

默认情况下，引擎使用 `transform` CSS 属性。此项设置为 `false` 滚动像我们2007年，IE：使用 `top`/`left`（因而滚动需要绝对定位）。

By default the engine uses the `transform` CSS property. Setting this to `false` scrolls like we were in 2007, ie: using the `top`/`left` (and thus the scroller needs to be absolutely positioned).

滚动和敏感的内容如 Flash、iframes 和 videos这可能是有用的，但要注意的是：性能损失是巨大的。

This might be useful when scrolling sensitive content such as Flash, iframes and videos, but be warned: performance loss is huge.

Default: `true`

### <small>options.</small>useTransition

iScroll 使用过度完成动画（ 动力和反弹 ）。通过设置为 `false`，`requestAnimationFrame` 来代替。

iScroll uses CSS transition to perform animations (momentum and bounce). By setting this to `false`, `requestAnimationFrame` is used instead.

在现代浏览器上的差异几乎不明显。在较旧的设备转换执行更好。

On modern browsers the difference is barely noticeable. On older devices transitions perform better.

Default: `true`

### <small>options.</small>HWCompositing

此选项尝试通过添加 `translateZ( 0 )` 放在硬件层的滚动条变换 CSS 属性。这大大提高了性能特别是在移动端，但有些你可能需要禁用它（ 特别是如果你有太多的元素和硬件无法赶上）。

This option tries to put the scroller on the hardware layer by appending `translateZ(0)` to the transform CSS property. This greatly increases performance especially on mobile, but there are situations where you might want to disable it (notably if you have too many elements and the hardware can't catch up).

Default: `true`

如果不确定舍弃 iScroll 将决定什么是最佳的配置。为了获得最佳的性能上述所有选项应该被设置为 `true` （ 或者更好的让他们不确定，因为他们是自动设置为 `true`）。你可以试试如果你遇到打嗝和内存泄漏和他们一起玩。

<div class="important">
<p>If unsure leave iScroll decide what's the optimal config. For best performance all the above options should be set to <code>true</code> (or better leave them undefined as they are set to true automatically). You may try to play with them in case you encounter hiccups and memory leaks.</p>
</div>

<h2 id="basic-features">Basic features</h2>

### <small>options.</small>bounce

当 滚动 到边界它进行小幅反弹动画。禁用反弹可能帮助在旧设备上达到平滑的效果。

When the scroller meets the boundary it performs a small bounce animation. Disabling bounce may help reach smoother results on old or slow devices.

Default: `true`

### <small>options.</small>click

重写本机滚动 iScroll 具有压制一些默认的浏览器行为，例如鼠标事件。如果你希望你的应用响应 `click` 事件，你必须明确的将此项设置为 `true`。请注意，建议使用自定义 `tap` event 事件，而不是（ 见下文 ）。

To override the native scrolling iScroll has to inhibit some default browser behaviors, such as mouse clicks. If you want your application to respond to the *click* event you have to explicitly set this option to `true`. Please note that it is suggested to use the custom `tap` event instead (see below).

Default: `false`

### <small>options.</small>disableMouse<br/><small>options.</small>disablePointer<br/><small>options.</small>disableTouch

通过默认 iScroll 监听所有指针事件并响应所发生的第一个。这似乎是对资源的浪费，但功能检测已被证明相当不可靠，这收听到所有的方法是我们最安全的赌注宽浏览器/设备的兼容性。

By default iScroll listens to all pointer events and reacts to the first one that occurs. It may seem a waste of resources but feature detection has proven quite unreliable and this *listen-to-all* approach is our safest bet for wide browser/device compatibility.

如果你有一个内部机制，设备检查或你知道你的脚本将要运行，你可能需要禁止所有你不需要的事件（ 鼠标，指针和触摸事件）。

If you have an internal mechanism for device detection or you know in advance where your script will run on, you may want to disable all event sets you don't need (mouse, pointer or touch events).

例如， 禁止鼠标和指针事件：

For example to disable mouse and pointer events:

    var myScroll = new IScroll('#wrapper', {
        disableMouse: true,
        disablePointer: true
    });

Default: `false`

### <small>options.</small>eventPassthrough

有时你想要保留原生的垂直滚动但是又能添加水平滚动（ 可能是旋转木马）。设置为true，iscroll地区应对水平不尽人意只。垂直滑动会自然滚动整个页面。

Sometimes you want to preserve native vertical scroll but being able to add an horizontal iScroll (maybe a carousel). Set this to `true` and the iScroll area will react to horizontal swipes only. Vertical swipes will naturally scroll the whole page.

请参阅在移动设备上的 [事件传递演示](http://lab.cubiq.org/iscroll5/demos/event-passthrough/)。注意，这个可以被设置为 `horizontal` 逆的行为（ 自然的横向滚动， 垂直 iScoll）。

See [event passthrough demo](http://lab.cubiq.org/iscroll5/demos/event-passthrough/) on a mobile device. Note that this can be set to `'horizontal'` to inverse the behavior (native horizontal scroll, vertical iScroll).

### <small>options.</small>freeScroll

（当你需要水平和垂直滚动）这个是非常有用主要的二维滚动条。通常当你开始滚动在一个方向时另外一个方向将被锁定。

This is useful mainly on 2D scrollers (when you need to scroll both horizontally and vertically). Normally when you start scrolling in one direction the other is locked.

有时候你只是想无约束的自由移动。在这些情况下你可以设置此项为 `true` 。 见 [ 2D 滚动演示 ](http://lab.cubiq.org/iscroll5/demos/2d-scroll/)。

Sometimes you just want to move freely with no constrains. In these cases you can set this option to `true`. See [2D scroll demo](http://lab.cubiq.org/iscroll5/demos/2d-scroll/).

Default: `false`

### <small>options.</small>keyBindings

设置此项为 `true` 激活键盘（ 和远程控制 ）的相互作用。请参阅下面的 [键绑定](#key-bindings)获取更多的信息。

Set this to `true` to activate keyboard (and remote controls) interaction. See the [Key bindings](#key-bindings) section below for more information.

Default: `false`

### <small>options.</small>invertWheelDirection

有意义当鼠标滚轮支持被激活，在这种情况下，它只是反转滚动方向。 （即下降向上滚动，反之亦然）。

Meaningful when mouse wheel support is activated, in which case it just inverts the scrolling direction. (ie. going down scrolls up and vice-versa).

Default: `false`

### <small>options.</small>momentum

可以打开/关闭的动量动画执行当用户很快笔触在屏幕上。关闭这个选项极大地提高性能。

You can turn on/off the momentum animation performed when the user quickly flicks on screen. Turning this off greatly enhance performance.

Default: `true`

### <small>options.</small>mouseWheel

Listen to the mouse wheel event.

Default: `false`

### <small>options.</small>preventDefault

是否要的 `preventDefault()` ，当事件被触发。这应留给 `true`，除非你真的知道你在做什么。

Whether or not to `preventDefault()` when events are fired. This should be left `true` unless you really know what you are doing.

见 `preventDefaultException` 中的[高级功能](#advanced-features)，以获取更多的控制权的 preventDefault 行为。

See `preventDefaultException` in the [Advanced features](#advanced-features) for more control over the preventDefault behavior.

Default: `true`

### <small>options.</small>scrollbars

是否显示默认滚动条，查看更多 [滚动条](#scrollbar) 部分。

Wheter or not to display the default scrollbars. See more in the [Scrollbar](#scrollbar) section.

Default: `false`.

### <small>options.</small>scrollX<br/><small>options.</small>scrollY

默认情况下只有垂直滚动启用。如果你需要水平滚动你必须设置 `scrollX` 为 `true`。查看 [水平滚动演示](http://lab.cubiq.org/iscroll5/demos/horizontal/)。

By default only vertical scrolling is enabled. If you need to scroll horizontally you have to set `scrollX` to `true`. See [horizontal demo](http://lab.cubiq.org/iscroll5/demos/horizontal/).

See also the **freeScroll** option.

Default: `scrollX: false`, `scrollY: true`

需要注意的是 `scrollX/Y true` 具有相同的效果如 `overflow：auto`。设置一个方向 `false` 有助于腾出一些检查，因此 CPU 周期。

<div class="important">
<p>Note that <code>scrollX/Y: true</code> has the same effect as <code>overflow: auto</code>. Setting one direction to <code>false</code> helps to spare some checks and thus CPU cycles.</p>
</div>

### <small>options.</small>startX<br/><small>options.</small>startY

默认情况下 iScroll 开始从 `0,0` （ 左上角 ）的位置，你可以指示滚动开球的不同的位置。

By default iScroll starts at `0, 0` (top left) position, you can instruct the scroller to kickoff at a different location.

Default: `0`

### <small>options.</small>tap

设置为 `true` 让 iScroll发出一个自定义 `tap` 事件时，滚动区域被 点击/轻扫 但不滚动。

Set this to `true` to let iScroll emit a custom `tap` event when the scroll area is clicked/tapped but not scrolled.

这是建议的方式来处理用户点击交互的元素，要监听 tap 事件，你可以添加一个事件监听器因为你会做一个标准的事件，例子：

This is the suggested way to handle user interaction with clickable elements. To listen to the tap event you would add an event listener as you would do for a standard event. Example: 

    element.addEventListener('tap', doSomething, false); \\ Native
    $('#element').on('tap', doSomething); \\ jQuery
    
你也可以通过传递一个字符串自定义事件名称。例如：    

You can also customize the event name by passing a string. Eg:

    tap: 'myCustomTapEvent'

在这种情况下监听你的 `myCustomTapEvent`。

In this case you'd listen to `myCustomTapEvent`.

Default: `false`

<h2 id="scrollbars">Scrollbars</h2>

滚动条不仅仅是什么名字。事实上，在内部，它们被引用作为指标。

The scrollbars are more than just what the name suggests. In fact internally they are referenced as *indicators*.

一个指标监听滚轮位置，通常它只是显示了其相对于整个位置，但它能做的就是这么多。

An indicator listens to the scroller position and normally it just shows its position in relation to whole, but what it can do is so much more.

Let's start with the basis.

### <small>options.</small>scrollbars

正如我们在 [基本功能部分](#basic-features) 中提到有，你该怎么做才能激活灿烂的滚动条只有一件事，那有一件事是：

As we mentioned in the [Basic features section](#basic-features) there's only one thing that you got to do to activate the scrollbars in all their splendor, and that one thing is:

    var myScroll = new IScroll('#wrapper', {
        scrollbars: true
    });

当然，默认行为可以个性化。

Of course the default behavior can be personalized.

### <small>options.</small>fadeScrollbars

什么时候不用滚动条消失，离开这个 `false` 至备用资源。

When not in use the scrollbar fades away. Leave this to `false` to spare resources.

Default: `false`

### <small>options.</small>interactiveScrollbars

滚动条变为可拖动和用户可以与它进行交互。

The scrollbar becomes draggable and user can interact with it.

Default: `false`

### <small>options.</small>resizeScrollbars

根据包装和滚轮宽度/高度的比例的滚动条大小的变化。将其设置为 `false` 使滚动条固定的大小。这可能是在出现的自定义风格的滚动条有用([ 见下文 ](#styling-the-scrollbar)).

The scrollbar size changes based on the proportion between the wrapper and the scroller width/height. Setting this to `false` makes the scrollbar a fixed size. This might be useful in case of custom styled scrollbars ([see below](#styling-the-scrollbar)).

Default: `true`

### <small>options.</small>shrinkScrollbars

当滚动条滚动到边界以外会少量收缩。

When scrolling outside of the boundaries the scrollbar is shrunk by a small amount.

Valid values are: `'clip'` and `'scale'`.

`'clip'` 只是移动的容器外的指示灯，给人的感觉是，滚动条收缩，但它只是简单地移出屏幕。如果你能忍受在视觉效果上这个选项极大地提高了整体性能。

`'clip'` just moves the indicator outside of its container, the impression is that the scrollbar shrinks but it is simply moving out of the screen. If you can live with the visual effect this option **immensely improves overall performance**.

`'scale'` 关闭 `useTransition` 因此所有的动画都配有 `requestAnimationFrame` 。 指示器实际上市变化了尺寸和最终的结果是更好的眼睛。

`'scale'` turns off `useTransition` hence all animations are served with `requestAnimationFrame`. The indicator is actually varied in size and the end result is nicer to the eye.

Default: `false`

需要注意的是调整大小不能由 GPU 来执行，所以 `scale` 是所有的 CPU.
如果你的应用运行在多种设备上，我的建议是关闭这个选项设置为 `scale`, `clip` 和 `false` 基于平台的响应速度（ 例如：你可以将其设置为 `clip` 和桌面浏览器到旧的移动设备 `scale`）。

<div class="tip">
<p>Note that resizing can't be performed by the GPU, so <code>scale</code> is all on the CPU.</p>
<p>If your application runs on multiple devices my suggestion would be to switch this option to <code>'scale'</code>, <code>'clip'</code> or <code>false</code> based on the platform responsiveness (eg: on older mobile devices you could set this to <code>'clip'</code> and on desktop browser to <code>'scale'</code>).</p>
</div>

See the [scrollbar demo](http://lab.cubiq.org/iscroll5/demos/scrollbars/).

<h3 id="styling-the-scrollbar">Styling the scrollbar</h3>

所以你不喜欢默认的滚动条造型你认为自己可以做的更好，来帮助自己！ iScroll 使得装饰滚动条易如反掌。首先设置 `scrollbars` 选项为 `'custom'`。

So you don't like the default scrollbar styling and you think you could do better. Help yourself! iScroll makes dressing the scrollbar a snap. First of all set the `scrollbars` option to `'custom'`:

    var myScroll = new IScroll('#wrapper', {
        scrollbars: 'custom'
    });

然后使用以下CSS类样式的小杂种。

Then use the following CSS classes to style the little bastards.

* **.iScrollHorizontalScrollbar**,这个被施加到水平容器。实际上承载滚动条指示器的元素。
* **.iScrollVerticalScrollbar**, 和上面一样，只不过是应用于垂直容器。
* **.iScrollIndicator**, 实际的滚动条指示器。
* **.iScrollBothScrollbars**，这是容器中添加元素，滚动条显示。通常只有一个（ 水平或垂直）显示。

* **.iScrollHorizontalScrollbar**, this is applied to the horizontal container. The element that actually hosts the scrollbar indicator.
* **.iScrollVerticalScrollbar**, same as above but for the vertical container.
* **.iScrollIndicator**, the actual scrollbar indicator.
* **.iScrollBothScrollbars**, this is added to the container elements when both scrollbars are shown. Normally just one (horizontal or vertical) is visible.

The [styled scrollbars demo](http://lab.cubiq.org/iscroll5/demos/styled-scrollbars/) should make things clearer than my lousy explanation.

If you set `resizeScrollbars: false` you could make the scrollbar of a fixed size, otherwise it would be resized based on the scroller length.

Please keep reading to the following section for a revelation that will shake your world.

<h2 id="indicators">Indicators</h2>

All the scrollbar options above are in reality just wrappers to the low level `indicators` option. It looks more or less like this:

    var myScroll = new IScroll('#wrapper', {
        indicators: {
            el: [element|element selector]
            fade: false,
            ignoreBoundaries: false,
            interactive: false,
            listenX: true,
            listenY: true,
            resize: true,
            shrink: false,
            speedRatioX: 0,
            speedRatioY: 0,
        }
    });

### <small>options.indicators.</small>el

This is a mandatory parameter which holds a reference to the scrollbar container element. The first child inside the container will be the indicator. Note that the scrollbar can be anywhere on your document, it doesn't need to be inside the scroller wrapper. Do you start perceiving the power of such tool?

Valid syntax would be:

    indicators: {
        el: document.getElementById('indicator')
    }

Or simply:

    indicators: {
        el: '#indicator'
    }

### <small>options.indicators.</small>ignoreBoundaries

This tells the indicator to ignore the boundaries imposed by its container. Since we can alter the speed ratio of the scrollbar, it is useful to just let the scrollbar go. Say you want the indicator to go twice as fast as the scroller, it would reach the end of its run very quickly. This option is used for [parallax scrolling](#parallax-scrolling).

Default: `false`

### <small>options.indicators.</small>listenX<br/><small>options.indicators.</small>listenY

To which axis the indicator listens to. It can be just one or both.

Default: `true`

### <small>options.indicators.</small>speedRatioX<br/><small>options.indicators.</small>speedRatioY

The speed the indicator moves in relation to the main scroller size. By default this is set automatically. You rarely need to alter this value.

Default: `0`

### <small>options.indicators.</small>fade<br/><small>options.indicators.</small>interactive<br/><small>options.indicators.</small>resize</br><small>options.indicators.</small>shrink

These are the same options we explored in the [scrollbars section](#scrollbars), I'm not going to insult your intelligence and repeat them here.

<div class="important">
<p><strong>Do not cross the streams. It would be bad!</strong> Do not mix the scrollbars syntax (<code>options.scrollbars</code>, <code>options.fadeScrollbars</code>, <code>options.interactiveScrollbars</code>, ...) with the indicators! Use one or the other.</p>
</div>

Have a look at the [minimap demo](http://lab.cubiq.org/iscroll5/demos/minimap/) to get a glance at the power of the `indicators` option.

The wittiest of you would have noticed that `indicators` is actually plural... Yes, exactly, passing an array of objects you can have a virtually infinite number of indicators. I don't know what you may need them for, but hey! who am I to argue about your scrollbar preferences?

## <span id="parallax-scrolling">Parallax scrolling</span>

Parallax scrolling is just a *collateral damage* of the [Indicators](#indicators) functionality.

An indicator is just a layer that follows the movement and animation applied to the main scroller. If you see it like that you'll understand the power behind this feature. To this add that you can have any number of indicators and the parallax scrolling is served.

Please refer to the [parallax demo](http://lab.cubiq.org/iscroll5/demos/parallax/).

## Scrolling programmatically

You silly! Of course you can scroll programmaticaly!

### scrollTo(x, y, time, easing)

Say your iScroll instance resides into the `myScroll` variable. You can easily scroll to any position with the following syntax:

    myScroll.scrollTo(0, -100);

That would scroll down by 100 pixels. Remember: 0 is always the top left corner. To scroll you have to pass negative numbers.

`time` and `easing` are optional. They regulates the duration (in ms) and the easing function of the animation respectively.

The easing functions are available in the `IScroll.utils.ease` object. For example to apply a 1 second elastic easing you'd do:

    myScroll.scrollTo(0, -100, 1000, IScroll.utils.ease.elastic);

The available options are: `quadratic`, `circular`, `back`, `bounce`, `elastic`.

### scrollBy(x, y, time, easing)

Same as above but X and Y are relative to the current position.

    myScroll.scrollBy(0, -10);
    
Would scroll 10 pixels down. If you are at -100, you'll end up at -110.

### scrollToElement(el, time, offsetX, offsetY, easing)

You're gonna like this. Sit tight.

The only mandatory parameter is `el`. Pass an element or a selector and iScroll will try to scroll to the top/left of that element.

`time` is optional and sets the animation duration.

`offsetX` and `offsetY` define an offset in pixels, so that you can scroll to that element plus a the specified offset. Not only that. If you set them to `true` the element will be centered on screen. Refer to the [scroll to element](http://lab.cubiq.org/iscroll5/demos/scroll-to-element/) example.

`easing` works the same way as per the **scrollTo** method.

<h2 id="snap">Snap</h2>

iScroll can snap to fixed positions and elements.

### <small>options.</small>snap

The simplest snap config is as follow:

    var myScroll = new IScroll('#wrapper', {
        snap: true
    });

This would automatically split the scroller into pages the size of the container.

`snap` also takes a string as a value. The string will be the selector to the elements the scroller will be snapped to. So the following

    var myScroll = new IScroll('#wrapper', {
        snap: 'li'
    });

would snap to each and every `LI` tag.

To help you navigate through the snap points iScroll grants access to a series of interesting methods.

### goToPage(x, y, time, easing)

`x` and `y` represent the page number you want to scroll to in the horizontal or vertical axes (yeah, it's the plural of *axis*, I checked). If the scroller in mono-dimensional, just pass `0` to the axis you don't need.

`time` is the duration of the animation, `easing` the easing function used to scroll to the point. Refer to the **option.bounceEasing** in the [Advanced features](#advanced-features). They are both optional.

    myScroll.goToPage(10, 0, 1000);

This would scroll to the 10th page on the horizontal axis in 1 second.

### next()<br/>prev()

Go to the next and previous page based on current position.

<h2 id="zoom">Zoom</h2>

To use the pinch/zoom functionality you better use the `iscroll-zoom.js` script.

### <small>options.</small>zoom

Set this to `true` to activate zoom.

Default: `false`

### <small>options.</small>zoomMax

Maximum zoom level.

Default: `4`

### <small>options.</small>zoomMin

Minimum zoom level.

Default: `1`

### <small>options.</small>zoomStart

Starting zoom level.

Default: `1`

### <small>options.</small>wheelAction

Wheel action can be set to `'zoom'` to have the wheel regulate the zoom level instead of scrolling position.

Default: `undefined` (ie: the mouse wheel scrolls)

To sum up, a nice zoom config would be:

    myScroll = new IScroll('#wrapper', {
        zoom: true,
        mouseWheel: true,
        wheelAction: 'zoom'
    });

<div class="important">
<p>The zoom is performed with CSS transform. iScroll can zoom only on browsers that support that.</p>
</div>

<div class="tip">
<p>Some browsers (notably webkit based ones) take a snapshot of the zooming area as soon as they are placed on the hardware compositing layer (say as soon as you apply a transform to them). This snapshot is used as a texture for the zooming area and it can hardly be updated. This means that your texture will be based on elements at <strong>scale 1</strong> and zooming in will result in blurred, low definition text and images.</p>

<p>A simple solution is to load content at double (or triple) its actual resolution and scale it down inside a <code>scale(0.5)</code> div. This should be enough to grant you a better result. I hope to be able to post more demos soon</p>
</div>

Refer to the [zoom demo](http://lab.cubiq.org/iscroll5/demos/zoom/).

### zoom(scale, x, y, time)

Juicy method that lets you zoom programmatically.

`scale` is the zoom factor.

`x` and `y` the focus point, aka the center of the zoom. If not specified, the center of the screen will be used.

`time` is the duration of the animation in milliseconds (optional).

<h2 id="infinite-scrolling">Infinite scrolling</h2>

iScroll integrates a smart caching system that allows to handle of a virtually infinite amount of data using (and reusing) just a bunch of elements.

Infinite scrolling is in an early stage of development and although it can be considered stable, it is not ready for wide consumption.

Please review the [infinite demo](http://lab.cubiq.org/iscroll5/demos/infinite/) and send your suggestions and bug reports.

I will add more details as soon as the functionality evolves.

<h2 id="advanced-options">Advanced options</h2>

For the hardcore developer.

### <small>options.</small>bindToWrapper

The `move` event is normally bound to the document and not the scroll container. When you move the cursor/finger out of the wrapper the scrolling keeps going. This is usually what you want, but you can also bind the move event to wrapper itself. Doing so as soon as the pointer leaves the container the scroll stops.

Default: `false`

### <small>options.</small>bounceEasing

Easing function performed during the bounce animation. Valid values are: `'quadratic'`, `'circular'`, `'back'`, `'bounce'`, `'elastic'`. See the [bounce easing demo](http://lab.cubiq.org/iscroll5/demos/bounce-easing/), drag the scroller down and release.

`bounceEasing` is a bit smarter than that. You can also feed a custom easing function, like so:

    bounceEasing: {
        style: 'cubic-bezier(0,0,1,1)',
        fn: function (k) { return k; }
    }

The above would perform a linear easing. The `style` option is used every time the animation is executed with CSS transitions, `fn` is used with `requestAnimationFrame`. If the easing function is too complex and can't be represented by a cubic bezier just pass `''` (empty string) as `style`.

Note that `bounce` and `elastic` can't be performed by CSS transitions.

Default: `'circular'`

### <small>options.</small>bounceTime

Duration in millisecond of the bounce animation.

Default: `600`

### <small>options.</small>deceleration

This value can be altered to change the momentum animation duration/speed. Higher numbers make the animation shorter. Sensible results can be experienced starting with a value of `0.01`, bigger than that basically doesn't make any momentum at all.

Default: `0.0006`

### <small>options.</small>mouseWheelSpeed

Set the speed of the mouse wheel.

Default: `20`

### <small>options.</small>preventDefaultException

These are all the exceptions when `preventDefault()` would be fired anyway despite the **preventDefault** option value.

This is a pretty powerful option, if you don't want to `preventDefault()` on all elements with *formfield* class name for example, you could pass the following:

    preventDefaultException: { className: /(^|\s)formfield(\s|$)/ }

Default: `{ tagName: /^(INPUT|TEXTAREA|BUTTON|SELECT)$/ }`.

### <small>options.</small>resizePolling

When you resize the window iScroll has to recalculate elements position and dimension. This might be a pretty daunting task for the poor little fella. To give it some rest the polling is set to 60 milliseconds.

By reducing this value you get better visual effect but the script becomes more aggressive on the CPU. The default value seems a good compromise.

Default: `60`

<h2 id="refresh">Mastering the refresh method</h2>

iScroll needs to know the exact dimensions of both the wrapper and the scroller. They are computed at start up but if your elements change in size, we need to tell iScroll that you are messing with the DOM.

This is achieved by calling the `refresh` method with the right timing. Please follow me closely, understanding this will save you hours of frustration.

Every time you touch the DOM the browser renderer repaints the page. Once this repaint has happened we can safely read the new DOM properties. The repaint phase is not instantaneous and it happens only at the end of the scope that triggered it. That's why we need to give the renderer a little rest before refreshing the iScroll.

To ensure that javascript gets the updated properties you should defer the refreh with something like this:

    ajax('page.php', onCompletion);

    function onCompletion () {
        // Update here your DOM
        
        setTimeout(function () {
            myScroll.refresh();
        }, 0);
    };

We have placed the `refresh()` call into a zero timeout. That is likely all you need to correctly refresh the iScroll boundaries. There are other ways to wait for the repaint, but the zero-timeout has proven pretty solid.

<div class="tip">
<p>Consider that if you have a very complex HTML structure you may give the browser some more rest and raise the timeout to 100 or 200 milliseconds.</p>

<p>This is generally true for all the tasks that have to be done on the DOM. Always give the renderer some rest.</p>
</div>

<h2 id="custom-events">Custom events</h2>

iScroll also emits some useful custom events you can hook to.

To register them you use the `on(type, fn)` method.

    myScroll = new IScroll('#wrapper');
    myScroll.on('scrollEnd', doSomething);

The above code executes the `doSomething` function every time the content stops scrolling.

The available types are:

* **beforeScrollStart**, executed as soon as user touches the screen but before the scrolling has initiated.
* **scrollCancel**, scroll initiated but didn't happen.
* **scrollStart**, the scroll started.
* **scroll**, the content is scrolling. Available only in `scroll-probe.js` edition. See [onScroll event](#onscroll).
* **scrollEnd**, content stopped scrolling.
* **flick**, user flicked left/right.
* **zoomStart**, user started zooming.
* **zoomEnd**, zoom ended.

<h2 id="onscroll">onScroll event</h2>

The `scroll` event is available on **iScroll probe edition** only (`iscroll-probe.js`). The probe behavior can be altered through the `probeType` option.

### <small>options.</small>probeType

This regulates the probe aggressiveness or the frequency at which the `scroll` event is fired. Valid values are: `1`, `2`, `3`. The higher the number the more aggressive the probe. The more aggressive the probe the higher the impact on the CPU.

`probeType: 1` has no impact on performance. The `scroll` event is fired only when the scroller is not busy doing its stuff.

`probeType: 2` always executes the `scroll` event except during momentum and bounce. This resembles the native `onScroll` event.

`probeType: 3` emits the `scroll` event with a to-the-pixel precision. Note that the scrolling is forced to `requestAnimationFrame` (ie: `useTransition:false`).

Please see the [probe demo](http://lab.cubiq.org/iscroll5/demos/probe/).

<h2 id="key-bindings">Key bindings</h2>

You can activate support for keyboards and remote controls with the `keyBindings` option. By default iScroll listens to the arrow keys, page up/down, home/end but they are (wait for it) totally customizable.

You can pass an object with the list of key codes you want iScroll to react to.

The default values are as follow:

    keyBindings: {
        pageUp: 33,
        pageDown: 34,
        end: 35,
        home: 36,
        left: 37,
        up: 38,
        right: 39,
        down: 40
    }

You can also pass a string (eg: `pageUp: 'a'`) and iScroll will convert it for you. You could just think of a key code and iScroll would read it out of your mind.

<h2 id="scroller-info">Useful scroller info</h2>

iScroll stores many useful information that you can use to augment your application.

You will probably find useful:

* **myScroll.x/y**, current position
* **myScroll.directionX/Y**, last direction (-1 down/right, 0 still, 1 up/left)
* **myScroll.currentPage**, current snap point info

These pieces of information may be useful when dealing with custom events. Eg:

    myScroll = new IScroll('#wrapper');
    myScroll.on('scrollEnd', function () {
        if ( this.x < -1000 ) {
            // do something
        }
    });

The above executes some code if the `x` position is lower than -1000px when the scroller stops. Note that I used `this` instead of `myScroll`, you can use both of course, but iScroll passes itself as `this` context when firing custom event functions.

<h2 id="destroy">Destroy</h2>

The public `destroy()` method can be used to free some memory when the iScroll is not needed anymore.

    myScroll.destroy();
    myScroll = null;

<h2 id="contributing">Contributing and CLA</h2>

If you want to contribute to the iScroll development, before I can accept your submission I have to ask you to sign the [Contributor License Agreement](http://cubiq.org/iscroll/cla/). Unfortunately that is the only way to enforce the openness of the script.

As an end user you have to do nothing of course. Actually the CLA ensures that nobody will even come after you asking for your first born for using the iScroll.

Please note that pull requests may take some time to be accepted. Testing iScroll is one of the most time consuming tasks of the project. iScroll works from desktop to smartphone, from tablets to smart TVs. I do not have physical access to all the testing devices, so before I can push a change I have to make sure that the new code is working everywhere.

Critical bugs are usually applied very quickly, but enhancements and coding style changes have to pass a longer review phase. *Remember that this is still a side project for me.*

<h2 id="whos">Who is using iScroll</h2>

It's impossible to track all the websites and applications that use the iScroll. It has been spotted on: Apple, Microsoft, People, LinkedIn, IKEA, Nike, Playboy, Bose, and countless others.

<h2 id="license">License (MIT)</h2>


Copyright (c) 2014 Matteo Spinelli, [cubiq.org](http://cubiq.org/)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
