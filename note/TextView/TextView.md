## 内容

1. [给文本加下划线](#给文本加下划线)
2. [设置文本可垂直滚动](#滚动)
3. [更新文字时自动滚动到最后一行](#更新文字时自动滚动到最后一行)
4. [改变局部文字的颜色](#改变局部文字颜色)

## <a id = "给文本加下划线">给文本加下划线</a>

### 方法一：在资源文件里加下划线

```xml
<resources>
    <string name="hello"><u>phone:0123456</u></string>
    <string name="app_name">MyLink</string>
</resources>
```

### 方法二：代码中加下划线

```java
TextView textView = (TextView)findViewById(R.id.tv_test); 
textView.setText(Html.fromHtml("<u>"+"0123456"+"</u>"));

```

或者

```java
tvTest.getPaint().setFlags(Paint. UNDERLINE_TEXT_FLAG ); //下划线
tvTest.getPaint().setAntiAlias(true);//抗锯齿

```

## <a id = "滚动">设置文本可垂直滚动</a>

### 方法一：给  TextView  控件设置  setMovementMethod  方法 

```java
// step1 在TextView控件中添加属性:
android:maxLines="15"
android:scrollbars="vertical"

// step2 java代码中添加代码:
mTextView.setMovementMethod(new ScrollingMovementMethod());

```

### 方法二：直接在 TextView 控件外面嵌套 ScrollView 控件即可.

```xml
<ScrollView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:scrollbars="none">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Hello worlds"/>
 </ScrollView>

```

## <a id = "更新文字时自动滚动到最后一行">更新文字时自动滚动到最后一行</a>

1. 在 TextView 的 xml 控件中 加入以下属性:

   ```xml
   android:scrollbars="vertical"  // 设置scrollbars属性为vertical
   android:scrollbarStyle="insideOverlay" // scroll样式 
   android:scrollbarFadeDuration="2000" // scrollbar从出现到消失的时间
   
   ```

   

2. java 代码中添加:

   ```java
   // 设置可滚动
   mResultTv.setMovementMethod(ScrollingMovementMethod.getInstance());
   
   ```

   

3. 实现 TextView 的刷新，将 TextView 滚动到最后一行。

   ```java
   private void refreshAlarmView(TextView textView,String msg){
       textView.append(msg);
       int offset=textView.getLineCount()*textView.getLineHeight();
       if(offset>(textView.getHeight()-textView.getLineHeight()-20)){
           textView.scrollTo(0,offset-textView.getHeight()+textView.getLineHeight()+20);
       }
   }
   
   ```

   参考地址[实现TextView的垂直滚动，更新文字时自动滚动到最后一行](https://blog.csdn.net/benbenxiongyuan/article/details/53454146)

## <a id = "改变局部文字颜色">改变局部文字颜色</a>

```kotlin
fun setTvColor(text: String, start: Int, tv: TextView, colorText: String) {
        val spannableString = SpannableString(text)
        spannableString.setSpan(
            ForegroundColorSpan(parseColor(colorText)),
            start,
            spannableString.length,
            Spanned.SPAN_EXCLUSIVE_EXCLUSIVE
        )
        tv.text = spannableString
 }
```

