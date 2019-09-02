# Flutter-UI

####设置 Android 状态栏变透明

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

