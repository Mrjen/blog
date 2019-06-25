```dart
class _StatelessWidgetDemoState extends State<StatelessWidgetDemo> {
  /// key
  GlobalKey _containerKey = GlobalKey();
  /// size
  Size _containerSize = Size(0, 0);
  /// Position
  Offset _containerPosition = Offset(0, 0);
  
  @override
  void initState() {
    super.initState();
 
    _getContainerSize();
 
    _getContainerPosition();
  }
 
  /// getSize
  _getContainerSize() {
    final RenderBox containerRenderBox =
        _containerKey.currentContext.findRenderObject();
    final containerSize = containerRenderBox.size;
    setState(() {
      _containerSize = containerSize;
    });
  }
 
  /// getPosition
  _getContainerPosition() {
    final RenderBox containerRenderBox =
        _containerKey.currentContext.findRenderObject();
    final containerPosition = containerRenderBox.localToGlobal(Offset.zero);
 
    setState(() {
      _containerPosition = containerPosition;
    });
  }
  
  @override
  Widget build(BuildContext context) {
    return SafeArea(
      Container(
        /// New
        key: _containerKey,
        width: 200,
        height: 200,
        color: Colors.red,
      ),
      /// New
      Text('Size: width = ${_containerSize.width} - height = ${_containerSize.height}'),
      /// New
      Text('Position: x = ${_containerPosition.dx} - y = ${_containerPosition.dy}'),        
     );
  }
}
```

