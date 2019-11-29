## 内容

1. [onItemClick事件无效](#onItemClick事件无效)
2. [内容被底部弹出UI遮挡](#内容被底部弹出UI遮挡)
3. [包含checkbox按钮](#包含checkbox按钮)
4. [setSelection无效的解决方案](#setSelection无效的解决方案)
5. [分割线显示和隐藏](#分割线显示和隐藏)
6. [其他问题](https://blog.csdn.net/jdfkldjlkjdl/article/details/82259823)

##  <a id ="onItemClick事件无效">onItemClick事件无效</a>

原因: listview 的 item 里面包含 button 或者 imageview 时,给 listview 设置 onitemlongclick 事件无效

解决: 添加属性 listviewitemandroid:descendantFocusability="blocksDescendants"

## <a id ="内容被底部弹出UI遮挡">内容被底部弹出UI遮挡</a>

```xml-dtd
在使用 listView 显示聊天窗口时，弹出输入法，listview 不会自动向上滚动，会遮盖内容，在manifest 中的 Activity加入：
android:windowSoftInputMode="adjustResize"
如果还是不行,还可以继续给ListView设置如下三个属性:
android:fastScrollEnabled="true"
android:scrollbarStyle="insideInset"
android:transcriptMode="normal"

```

## <a id = "包含checkbox按钮">包含checkbox按钮</a>

```xml-dtd
1.item根布局添加属性 android:descendantFocusability="blocksDescendants"
2.checkgox标签如下
<CheckBox
android:id="@+id/cb_checkbox"
style="@style/ChatCheckboxTheme"
android:layout_width="30dp"
android:layout_height="30dp"
android:layout_alignParentRight="true"
android:layout_marginRight="25dp"
android:layout_marginTop="0dp"
android:gravity="center"
/>
Checkbox 无需额外添加属性
Checkbox 的点击事件可通过在适配器中采用回调来实现。

```

## <a id ="setSelection无效的解决方案">setSelection无效的解决方案</a>

```java
原因一：界面初始化完成之后listview失去了焦点。
原因二：因为listview的item高度不一致，或者添加了headerview，在setadapter之后调用setSelection无法准确定位。

万能解决方法：
final ListView listView = new ListView(getActivity());
listView.post(new Runnable() {
    @Override
    public void run() {
        listView.requestFocusFromTouch();//获取焦点
         listView.setSelection(listView.getHeaderViewsCount()+10);//10是你需要定位的位置
    }
});

如果还是不行则:
final ListView listView = new ListView(getActivity());
listView.postDelayed(new Runnable() {
    @Override
    public void run() {
        listView.requestFocusFromTouch();
        listView.setSelection(listView.getHeaderViewsCount()+10);
    }
},500);

```

## <a id ="分割线显示和隐藏">分割线显示和隐藏</a>

```java
1. 设置和取消每个item分隔线
解决方案：
ListView.setDivider(null)；
android:Divider="@null";
android:divider="@drawable/listview_horizon_line"
Android:divider= “@color/color”

2. 隐藏头部分隔线

listview分割线会在头部、数据item、及根部的底部打印，如果要取消头部分割线必须
先设置期方法
  addHeaderView(headView, null, true);
  addFooterView(footView, null, true);
注意：第三个参数必须为true，否则无效
//显示头部出现分割线
listview.setHeaderDividersEnabled(true);
//禁止底部出现分割线 
listview.setFooterDividersEnabled(false);

```

