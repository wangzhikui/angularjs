# SASS特性

**算术操作符**:	加、减、乘、除、取余。

上面的操作符只能用于单位相同的数值运算
h2 {
    font-size: 5px + 2em; // 单位不一致，编译报错
    font-size: 5px + 2; // 7px
}
两个单位相同的数值相乘无法生成有效的 CSS
h2 {
    font-size: 5px * 2px; // 10px*px isn't a valid CSS value
}
+ 操作符也可以用来拼接字符串,拼接规则：
如果字符串被引号包裹，那么它拼接任何字符串的结果也会被引号包裹
如果字符串没有被引号包裹，那么它拼接任何字符串的结果也不会被引号包裹
@mixin string-concat {
        content: "My favorite language is " + Sass;//content: "My favorite language is Sass";
        font: Arial + " sans-serif " +Sass;//font: Arial sans-serif Sass;
}

h2 {
    @include string-concat;
}

**逻辑操作符**
and、or、not

$list-map: (success: lightgreen, alert: tomato, info: lightblue);//定义一个map

@mixin button-state($btn-state) {
    @if (length($list-map) > 2 or length($list-map) < 5) {
        background-color: map-get($list-map, $btn-state);
    }
}

.btn {
    @include button-state(success);
}

**颜色运算**
h2 {
    color: #468499 + #204479;//color: #66c8ff;
}

h2 {
    color: rgba(70, 132, 153, 1) + rgba(32, 68, 121, 1);

    color: rgba(70, 132, 153, .9) + rgba(32, 68, 121, .7);
    // 报错，透明通道的值必须一致
}
RGB色彩模式+alpha透明度
以上R、G、B三个参数，正整数值的取值范围为：0 - 255,百分数值的取值范围为：0.0% - 100.0%
IE9以下不支持百分数值

使用算术操作符处理 rgba() 和 hsla() 时，必须让透明通道的值保持一致
HSLA
H：Hue(色调)。0(或360)表示红色，120表示绿色，240表示蓝色，也可取其他数值来指定颜色。取值为：0 - 360
S：Saturation(饱和度)。取值为：0.0% - 100.0%
L：Lightness(亮度)。取值为：0.0% - 100.0%
A：Alpha透明度。取值0~1之间。

**Map**
Sass的map使用一个括号，并用冒号将键值与值分隔开来，并且使用逗号将一对键值/值隔开
map中的最后一对键值/值后面的逗号可以省略
键值必须是唯一的
键值/值可以是Sass的任何类型，包括列表和其他的Sass map

在Sass中map自身带了七个函数
map-get($map,$key)：根据给定的key值，返回map中相关的值。
map-merge($map1,$map2)：将两个map合并成一个新的map。
map-remove($map,$key)：从map中删除一个key，返回一个新map。
map-keys($map)：返回map中所有的key。
map-values($map)：返回map中所有的value。
map-has-key($map,$key)：根据给定的key值判断map是否有对应的value值，如果有返回true，否则返回false。
keywords($args)：返回一个函数的参数，这个参数可以动态的设置key和value。
实例
$breakpoint-map: (
  small: (
    min-width: null,
    max-width: 479px,
    base-font: 16px,
    vertical-rhythm: 1.3
  ),
  medium: (
    min-width: 480px,
    max-width: 959px,
    base-font: 18px,
    vertical-rhythm: 1.414
  ),
  large: (
    min-width: 960px,
    max-width: 1099px,
    base-font: 18px,
    vertical-rhythm: 1.5
  ),
  xlarge: (
    min-width: 1100px,
    max-width: null,
    base-font: 21px,
    vertical-rhythm: 1.618
  )
);

// Its loops would look like this:
@each $label, $map in $breakpoint-map {
  $min-width: map-get($map, min-width);
  $max-width: map-get($map, max-width);
  $base-font: map-get($map, base-font);
  $vertical-rhythm: map-get($map, vertical-rhythm);
}