# Flutter开发中的几个常用函数

```dart
/** 返回当前时间戳 */
  static int currentTimeMillis() {
    return new DateTime.now().millisecondsSinceEpoch;
  }

  /** 复制到剪粘板 */
  static copyToClipboard(final String text) {
    if (text == null) return;
    Clipboard.setData(new ClipboardData(text: text));
  }

  static const RollupSize_Units = ["GB", "MB", "KB", "B"];
  /** 返回文件大小字符串 */
  static String getRollupSize(int size) {
    int idx = 3;
    int r1 = 0;
    String result = "";
    while (idx >= 0) {
      int s1 = size % 1024;
      size = size >> 10;
      if (size == 0 || idx == 0) {
        r1 = (r1 * 100) ~/ 1024;
        if (r1 > 0) {
          if (r1 >= 10)
            result = "$s1.$r1${RollupSize_Units[idx]}";
          else
            result = "$s1.0$r1${RollupSize_Units[idx]}";
        } else
          result = s1.toString() + RollupSize_Units[idx];
        break;
      }
      r1 = s1;
      idx--;
    }
    return result;
  }
```



```dart
/** 返回两个日期相差的天数 */
  static int daysBetween(DateTime a, DateTime b, [bool ignoreTime = false]) {
    if (ignoreTime) {
      int v = a.millisecondsSinceEpoch ~/ 86400000 -
          b.millisecondsSinceEpoch ~/ 86400000;
      if (v < 0) return -v;
      return v;
    } else {
      int v = a.millisecondsSinceEpoch - b.millisecondsSinceEpoch;
      if (v < 0) v = -v;
      return v ~/ 86400000;
    }
  }
```



```dart
  static double getScreenWidth(BuildContext context) {
    return MediaQuery.of(context).size.width;
  }

  /** 获取屏幕高度 */
  static double getScreenHeight(BuildContext context) {
    return MediaQuery.of(context).size.height;
  }

  /** 获取系统状态栏高度 */
  static double getSysStatsHeight(BuildContext context) {
    return MediaQuery.of(context).padding.top;
  }
```

```dart
 /** dart 日期格式化*/
  DateTime today = new DateTime.now();
  String dateSlug ="${today.year.toString()}-${today.month.toString().padLeft(2,'0')}-${today.day.toString().padLeft(2,'0')}";
  print('dateSlug${dateSlug}');
```

```dart
 /** 清除定时器*/
 var timer = new Timer(new Duration(seconds: 1), () => print('done'));
 timer.cancel();
```

```dart
 /** 时间差倒计时*/
checkTime(int i) {
    return i < 10 ? '0${i.toString()}' : i;
  }

  showTime() {
    int now = new DateTime.now().millisecondsSinceEpoch; // 当前时间戳
    int endtime = 1555387932; // 结束时间
    int diff = (endtime - (now / 1000)).toInt();
    var timer;
    if(diff < 0 || diff == 0) {
      print('倒计时已结束'); 
      try{  
        timer.cancel(); 
      }catch(e){}
    } else {
      int day = (diff~/60~/60~/24);     
      int hour = (diff~/60~/60%24).toInt();
      int minute = (diff~/60%60).toInt();
      int second = (diff%60).toInt();
      String leftTime = '${day}天${checkTime(hour)}时${checkTime(minute)}分${checkTime(second)}秒';
      print('还剩${leftTime}');
      timer = new Future.delayed(const Duration(seconds: 1), (){
        showTime();
      });
    }
  }
```

```dart
/** 关闭键盘 */
FocusScope.of(context).requestFocus(new FocusNode());
```
