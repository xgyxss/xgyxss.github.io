---
title: flutter报错处理-三
date: 2022-04-28 14:19:49
tags: [flutter, 报错处理, 202204]
categories: 解决方案
---

- <a href="#target">The argument type 'Null' can't be assigned to the parameter type 'Key'.</a>

<!-- more -->

### <a name="target">The argument type 'Null' can't be assigned to the parameter type 'Key'.</a>

```dart
import 'dart:math';

import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter Demo'),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({required Key? key, required this.title}) : super(key: key);
  final String title;

  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  int _number = 0;
  void _incrementCounter() {
    _number = Random().nextInt(100);
    setState(() {});
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Center(
        child: InfoWidget(
          number: _number,
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                InfoChildWidget(),
                InfoChildWidget(),
                InfoChildWidget(),
              ],
            ),
          ),
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Increment',
        child: Icon(Icons.add),
      ),
    );
  }
}

// <!-- InfoWidget -->
class InfoWidget extends InheritedWidget {
  final int number;

  InfoWidget({required Key key, required this.number, @required child})
      : super(key: key, child: child);

  @override
  bool updateShouldNotify(InfoWidget oldWidget) {
    return number != oldWidget.number;
  }

  static InfoWidget? of(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType();
  }
}

// <!-- InfoChildWidget -->
class InfoChildWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final int? number = InfoWidget.of(context)?.number;
    return Text("$number", style: TextStyle(color: Colors.amber, fontSize: 40));
  }
}
```

第13行 MyHomePage 报错：`The named parameter 'key' is required, but there's no corresponding argument.`

第40行 InfoWidget 报错：`The named parameter 'key' is required, but there's no corresponding argument. `（命名参数 key 是必须的，但是没有对应的参数。）

> 这个错误的出现是因为用了`required`关键字。如果想传递一个空值作为 key，可以像这样改造构造函数：
>
> `MyWidget({Key? key}) : super(key: key);`

第 19 行 改成：`MyHomePage({Key? key, required this.title}) : super(key: key);`；

第 67、68 行 改成：`InfoWidget({Key? key, required this.number, @required child})
    : super(key: key, child: child);`。
