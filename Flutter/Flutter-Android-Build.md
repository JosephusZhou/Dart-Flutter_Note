# Flutter-Android-Build

* #### 对 Android 模块指定编译输出 apk 文件名后运行报错

在`build.gradle`中指定 apk 输出名和路径：

```groovy
applicationVariants.all { variant ->
        variant.outputs.all {
            def apkName = 'App-' + versionName
            outputFileName = apkName + '.apk'
        }
    }
```

报错信息：

```
Finished with error: Gradle build failed to produce an Android package.
```

查询 issues 后发现出现问题的情况有两种，一种是 abi 分包，一种是我上面的指定输出 apk名称。问题在于修改名字后 Flutter 找不到了，定位不到 apk 位置所以报错了。

issues 上暂时找不到解决方法~

