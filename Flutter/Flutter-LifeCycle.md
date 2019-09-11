# Flutter-LifeCycle

* #### Flutter 如何监听 `onResume()`、`onPause()` 等类似 Android 页面生命周期方法

由于 Flutter中`万物皆为 Widget`，所以每个页面的方法无非是 `initState()`、`dispose()` 和 `build（）`等组件方法。实际业务中总会有需要在不同页面生命周期进行处理的要求，可以通过添加`WidgetsBindingObserver`来监听组件的生命周期。

有个注意的地方，首次进入页面时，有绑定操作，第一次的`resumed`事件是捕获不到的，需要进入页面初始化一些操作的话，可以在`initState()`、或者`build()`并结合标志位变量的方式来达到一次性初始化的目的。

有些操作在`initState()`无法完成，因为此时组件还未渲染构建。

```dart
class AppLifecycleReactor extends StatefulWidget {
  const AppLifecycleReactor({ Key key }) : super(key: key);

  @override
  _AppLifecycleReactorState createState() => _AppLifecycleReactorState();
}

class _AppLifecycleReactorState extends State<AppLifecycleReactor> with WidgetsBindingObserver {
  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addObserver(this);
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(this);
    super.dispose();
  }

  AppLifecycleState _notification;

  @override
  void didChangeAppLifecycleState(AppLifecycleState state) {
    setState(() { _notification = state; });
  }

  @override
  Widget build(BuildContext context) {
    return Text('Last notification: $_notification');
  }
}
```

