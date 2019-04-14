```dart
/**页面滚动顶部导航栏渐变消失*/
_scrollEvent(offset) {
  double alpha = offset / MAX_SCROLL_HEIGHT; // 最大滚动高度
  if(alpha < 0) {
    alpha = 0;
  } else if (alpha > 1) {
    alpha = 1;
  }
  setState(() {
    appBarAlpha = alpha; // AppBar透明度
  });
}

return Scaffold(
      body: MediaQuery.removePadding(
        removeTop: true,
        context: context,
        child: Stack(
          children: <Widget>[
            NotificationListener(
              onNotification: (ScrollNotification){
                if(ScrollNotification is ScrollUpdateNotification && ScrollNotification.depth == 0) {
                  print('我滚动了${ScrollNotification}');
                  _scrollEvent(ScrollNotification.metrics.pixels);
                }
              },
              child: ListView.builder(
                itemCount: 50,
                itemBuilder: (context, index){
                  return Container(
                    width: 375,
                    height: 100,
                    decoration: BoxDecoration(
                      color: Colors.grey,
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
            ),
            Opacity(
              opacity: appBarAlpha,
              child: Container(
                width: 500,
                height: 80,
                decoration: BoxDecoration(
                  color: Colors.red,
                ),
                child: Center(
                  child: Padding(
                    padding: EdgeInsets.only(top: 20.0),
                    child: Text('首页'),
                  ),
                ),
              ),
            ),
          ],
        )
      ),
    );
```
