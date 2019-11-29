## 内容

1. [判断当前 Fragment 是否可见](#是否可见)
2. 

## <a id = "是否可见">是否可见</a>

```java
/** Fragment当前状态是否可见 */
    protected boolean isVisible;

    @Override
    public void setUserVisibleHint(boolean isVisibleToUser) {
        super.setUserVisibleHint(isVisibleToUser);

        if(getUserVisibleHint()) {
            isVisible = true;
        } else {
            isVisible = false;
        }
    }

```

