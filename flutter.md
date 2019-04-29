Dart 

### **Null 类型检查**

 从Dart1.12开始，null-aware运算符就可以用作帮助我们做null做类型检查

```dart
bool isConnected(a, b) {
  bool outConn = outgoing[a]?.contains(b) ?? false
}
```

(?.) 运算符在左边为null的情况下会阻断右边的调用，(??) 运算符主要作用是在左侧表达式为null时为其设置默认值

对于表达式：

```dart
outgoing[a]?.contains(b)
```

如果outging为null或outging[a]为null或contains(b)的值为null，都会导致表达式为null。



### 如何创建可复用的Widget

在Flutter中，需要定义一个类来创建自定义Widget，然后复用widget。还可以定义和调用返回可重用小部件的函数，如下：

```dart
calss CustomCard extends StatelessWidget {
  CustomCard({@required this.index, @required this.onPress});
  final index;
  final Function onPress;
  
  @override
  WidgetBuild(BuildContext context) {
    return Card(
      child: Column(
        children: <Widget>[
          Text('Card $index'),
          FlatButton(
            child: Text('Press'),
            onPressed: this,onPress
          )
        ]
      )
    )
  }
}


// Use
CustomCard(
	index: index,
  onPress:(){
    print('Card $index');
  }
)
```



### CurvedAnimation

CurvedAnimation将动画过程第一位一个非线性曲线。

```dart
final CurvedAnimation curve = CurvedAnimation(parent: controller, curve: Curves.easeIn);
```

注：Curves类定义了许多常用的曲线，也可以创建自己的，例如：

```dart
class AshakeCurve extends Curve{
  @overried
  double transform(double t) {
    return math.sin(t * math.PI * 2);
  }
}
```



```dart
Class GrowTransition extends StatelessWidget {
  Growtransition({this.child, this.animation});
  final Widget child;
  final Animation<double> animation;
  widget build(BuildContext context) => Center(
    child: AnimatedBuilder(
    	animation: animation,
    	builder: (context, child) => Container(
    		height: animation.value,
    		width: animation.value,
    		child: child
    	),
    	child: child
    )
  )
}
```





```dart
return Scaffold(
      body: MediaQuery.removePadding( // 移除padding
        removeTop: true,  
        context: context,
        child: NotificationListener( // 监听滚动
          onNotification: (ScrollNotification){
            if(ScrollNotification is ScrollUpdateNotification 
               && ScrollNotification.depth == 0) {
                print('我滚动了${ScrollNotification}');
            }
          },
          child: ListView.builder(
            itemCount: 50,
            itemBuilder: (context, index){
              return Container(
                width: 375,
                height: 100,
                decoration: BoxDecoration(
                  color: Colors.green,
                  border: Border(
                    bottom: BorderSide(
                      width: 1,
                      color: Colors.red,
                    )
                  ),
                ),
                child: Text('我是第${index}个'),
              );
            },
          ),
        )
      ),
    );
```

```dart
  /**flutter 修复*/  flutter根目录运行一下命令
  
  git clean -xfd
  git stash save --keep-index
  git stash drop
  git pull
  flutter doctor
```


