# DragGesture

```swift
struct ContentView: View {
    @State var dragState = CGSize.zero //储存状态
    var body: some View {
            RoundedRectangle(cornerRadius: 10)
            .fill(Color.blue)
            .frame(width: 200,height: 200)
            .offset(x:dragState.width,y: dragState.height)//更新元素的位置
            .gesture(
                DragGesture()
                    .onChanged({ value in
                        dragState = value.translation
                    }) //位置发生改变后，将新的位置信息赋给dragState
                    .onEnded({ _ in
                        withAnimation {
                            dragState = .zero
                        }
                    }) //拖动结束后回到原来位置 
 
                )
    }
}
```

`@State var dragState = CGSize.zero ` 存储初始位置状态， 初始值为`.zero` 表示没有便宜了。

`.offset(x:dragState.width,y: dragState.height)` 根据拖动的位置更新元素的偏移位置。



```swift
DragGesture()
	.onChanged({ value in
      dragState = value.translation
   }) //位置发生改变后，将新的位置信息赋给dragState
```

当拖拽后位置信息发生改变，将新的位置信息赋给`dragState`，然后通过`.offset(x:dragState.width,y: dragState.height)` 更新位置信息。



```swift
.onEnded({_ in
  withAnimation {
    dragState = .zero 
  }
})
```

拖拽手势结束后重置位置，并添加回弹动画。