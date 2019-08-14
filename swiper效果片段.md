```dart
  // 轮播左对齐效果
  import 'package:flutter/material.dart';

class MySwiper extends StatefulWidget {
  @override
  _MySwiperState createState() => _MySwiperState();

}

class _MySwiperState extends State<MySwiper> {
  
  final PageController ctrl = PageController(viewportFraction: 0.9);
  int currentPage = 0;
  String activeTag = 'favorites';

  List slideList = [
    'https://images.unsplash.com/photo-1565787113689-48b5f2853153?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1534&q=80',
    'https://images.unsplash.com/photo-1565736736511-c6aa88ad1c24?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1534&q=80',
    'https://images.unsplash.com/photo-1560237135-fb8529ec1d1b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1534&q=80',
    'https://images.unsplash.com/photo-1565732439215-c2facc176a3f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1532&q=80'
  ];

  @override
  void initState() {
    super.initState();

    ctrl.addListener((){
      int next = ctrl.page.round();
      if(currentPage != next) {
        setState(() {
          currentPage = next;
        });
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      child: PageView.builder(
        scrollDirection: Axis.horizontal,
        controller: ctrl,
        itemCount: 4,
        itemBuilder: (context, idx){
          if(idx == 0) {
            return Container(
              color: Colors.blue.withOpacity(.5),
              width: 375,
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                crossAxisAlignment: CrossAxisAlignment.start,
                children: <Widget>[
                  Text('menu001'),
                  Text('menu002'),
                  Text('menu003'),
                ],
              ),
            );
          }
          bool active = idx == currentPage;
          return _rightView(slideList[idx], active);
        },
      )
    );
  }

  Widget _rightView(String image, bool active) {
    
    final double blur = active ? 30 : 0;
    final double offset = active ? 20 : 0;
    final double top = active ? 50 : 0;

    return AnimatedContainer(
      duration: Duration(milliseconds: 500),
      curve: Curves.easeOutQuint,
      margin: EdgeInsets.only(
        top: top,
        bottom: 50,
        right: 30
      ),
      decoration: BoxDecoration(
        borderRadius: BorderRadius.circular(20),
        image: DecorationImage(
          image: NetworkImage(image),
          fit: BoxFit.cover
        ),
        boxShadow: [
          BoxShadow(
            color: Colors.black87,
            blurRadius: blur,
            offset: Offset(offset, offset)
          ),
        ]
      ),
      child: Center(
        child: Text('我是标题'),
      ),
    );
  }

  
}
```
