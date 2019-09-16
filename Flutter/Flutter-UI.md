# Flutter-UI

* #### 设置 Android 状态栏变透明

在 main() 函数中添加设置系统 UI 样式的代码：

```dart
void main() {
  runApp(MainApp());
  // Android 状态栏透明
  if (Platform.isAndroid) {
    SystemUiOverlayStyle systemUiOverlayStyle =
        SystemUiOverlayStyle(statusBarColor: Colors.transparent);
SystemChrome.setSystemUIOverlayStyle(systemUiOverlayStyle);
  }
}
```

* #### 移除滚动视图的水波纹效果

~~除非你的应用设计完全遵循 MD 风格，否则这玩意真的很丑~~

水波纹效果来自通过[`ScrollBehavior`](https://docs.flutter.io/flutter/widgets/ScrollBehavior-class.html)添加的[`GlowingOverscrollIndicator`](https://docs.flutter.io/flutter/widgets/GlowingOverscrollIndicator-class.html)。移除该效果只需要通过[`ScrollConfiguration`](https://docs.flutter.io/flutter/widgets/ScrollConfiguration-class.html)包裹 App 或者单一组件并指定自定义`ScrollBehavior`即可。

自定义`ScrollBehavior`：

```dart
class MyBehavior extends ScrollBehavior {
  @override
  Widget buildViewportChrome(
      BuildContext context, Widget child, AxisDirection axisDirection) {
    return child;
  }
}
```

全局移除：

```dart
MaterialApp(
  builder: (context, child) {
    return ScrollConfiguration(
      behavior: MyBehavior(),
      child: child,
    );
  },
  home: new MyHomePage(),
);
```

单一组件移除，比如`ListView`：

```dart
ScrollConfiguration(
  behavior: MyBehavior(),
  child: ListView(
    ...
  ),
)
```

* #### 自定义 MaterialColor

根据 Material Design 的指南，自定义一个 `MaterialColor` 需要十个的渐变颜色，对于没有艺术细胞的开发来说很痛苦，只能使用 `opacity` 这个不透明度属性来自定义，这样只需要一个色值就可以了。以下使用了中国传统颜色靛青来实现：

```dart
MaterialColor pColor = MaterialColor(
    0xFF177cb0,
    <int, Color>{
      50: Color.fromRGBO(23, 124, 176, .1),
      100: Color.fromRGBO(23, 124, 176, .2),
      200: Color.fromRGBO(23, 124, 176, .3),
      300: Color.fromRGBO(23, 124, 176, .4),
      400: Color.fromRGBO(23, 124, 176, .5),
      500: Color.fromRGBO(23, 124, 176, .6),
      600: Color.fromRGBO(23, 124, 176, .7),
      700: Color.fromRGBO(23, 124, 176, .8),
      800: Color.fromRGBO(23, 124, 176, .9),
      900: Color.fromRGBO(23, 124, 176, 1),
    },
  );
```

