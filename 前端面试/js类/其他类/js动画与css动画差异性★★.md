
# js动画与css动画差异性★★


使用动画 （js实现动画，css3实现动画）
+ 一个是帧动画 一个是补间动画
+ 什么是帧动画：使用定时器 每隔一段时间 更改当前元素的状态
+ 什么是补间动画：过渡(加过渡只要状态发生改变产出动画) 、 动画（多个节点来控制动画） ，性能会更好
+ 在支持H5C3的的浏览器尽可能使用css3动画 （移动端开发）

### CSS动画
#### 优点：

1、浏览器可以对动画进行优化。

（1） 浏览器使用与 requestAnimationFrame 类似的机制，requestAnimationFrame比起setTimeout，setInterval设置动画的优势主要是:1)requestAnimationFrame 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成,并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率,一般来说,这个频率为每秒60帧。2)在隐藏或不可见的元素中requestAnimationFrame不会进行重绘或回流，这当然就意味着更少的的cpu，gpu和内存使用量。

（2）强制使用硬件加速 （通过 GPU 来提高动画性能）

2、代码相对简单,性能调优方向固定

3、对于帧速表现不好的低版本浏览器，CSS3可以做到自然降级，而JS则需要撰写额外代码

#### 缺点：

1、 运行过程控制较弱,无法附加事件绑定回调函数。CSS动画只能暂停,不能在动画中寻找一个特定的时间点，不能在半路反转动画，不能变换时间尺度，不能在特定的位置添加回调函数或是绑定回放事件,无进度报告

2、 代码冗长。想用 CSS 实现稍微复杂一点动画,最后CSS代码都会变得非常笨重。

### JS动画
#### 优点：

1、JavaScript动画控制能力很强, 可以在动画播放过程中对动画进行控制：开始、暂停、回放、终止、取消都是可以做到的。

2、动画效果比css3动画丰富,有些动画效果，比如曲线运动,冲击闪烁,视差滚动效果，只有JavaScript动画才能完成

3、CSS3有兼容性问题，而JS大多时候没有兼容性问题

#### 缺点：

1、JavaScript在浏览器的主线程中运行，而主线程中还有其它需要运行的JavaScript脚本、样式计算、布局、绘制任务等,对其干扰导致线程可能出现阻塞，从而造成丢帧的情况。

2、代码的复杂度高于CSS动画

总结：如果动画只是简单的状态切换，不需要中间过程控制，在这种情况下，css动画是优选方案。它可以让你将动画逻辑放在样式文件里面，而不会让你的页面充斥 Javascript 库。然而如果你在设计很复杂的富客户端界面或者在开发一个有着复杂UI状态的 APP。那么你应该使用js动画，这样你的动画可以保持高效，并且你的工作流也更可控。所以，在实现一些小的交互动效的时候，就多考虑考虑CSS动画。对于一些复杂控制的动画，使用javascript比较可靠。





面试题目的参考：

渲染线程分为main thread和compositor thread，如果css动画只改变transform和opacity，这时整个CSS动画得以在compositor trhead完成（而js动画则会在main thread执行，然后出发compositor thread进行下一步操作），特别注意的是如果改变transform和opacity是不会layout或者paint的。

css比js动画流畅的原理是 因为在合成器线程中进行动画处理，所以节省了昂贵的主线程资源
