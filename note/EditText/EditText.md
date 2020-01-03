## 内容

1. [编辑框被输入法遮盖](https://blog.csdn.net/jdfkldjlkjdl/article/details/61913023)
2. [设置EditText的hint字体大小](#设置hint字体大小)
3. 

## <a id = "设置hint字体大小">设置hint字体大小</a>

```kotlin
/**
 * 设置EditText的hint字体大小
 *
 * @param editText EditText控件
 * @param hintText hint内容
 * @param size     hint字体大小，单位为sp
 */
fun setEditTextHintWithSize(editText: EditText, hintText: String?, @Dimension size: Int) {
    if (!TextUtils.isEmpty(hintText)) {
        val ss = SpannableString(hintText)
        //设置字体大小 true表示单位是sp
        val ass = AbsoluteSizeSpan(size, true)
        ss.setSpan(ass, 0, ss.length, Spanned.SPAN_EXCLUSIVE_EXCLUSIVE)
        editText.hint = SpannedString(ss)
    }
}
```

