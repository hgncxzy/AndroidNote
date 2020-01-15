## 内容

1. [新版本中添加了新表时注意事项](#新版本中添加了新表时注意事项)
2. [判断数据库中某个表是否存在(DBHelper中的方法)](#判断数据库中某个表是否存在)
3. [SQL 教程](https://www.w3school.com.cn/sql/index.asp)

## <a id = "新版本中添加了新表时注意事项">新版本中添加了新表时注意事项</a>

1. DBHelper中版本号加1

   (如果之前 vesion=2，那么该版本顺序加 1 version = 3),并在

    

   ```java
   onUpgrage(SQLiteDatabase db, int oldVersion, int newVersion) 
   ```

   中处理相关逻辑;

2. 方法中,需要检查新表是否存在，如果不存在，则创建该表，避免新版 app 覆盖旧版 app 安装时打开 app 闪退。

## <a id="判断数据库中某个表是否存在">判断数据库中某个表是否存在</a>

```java
public class DBHelper extends SQLiteOpenHelper {

    //数据库名
    public static final String FILE_NAME = "qlink.db";

    //数据库版本
    public static final int DB_VERSION = 5;

    private static DBHelper mInstance;

    public static DBHelper getInstance(Context context) {
        if (null == mInstance) {
            synchronized (DBHelper.class) {
                mInstance = new DBHelper(context.getApplicationContext());
            }
        }
        return mInstance;
    }

    private DBHelper(Context context) {
        this(context, FILE_NAME, DB_VERSION);
    }


    private DBHelper(Context context, String name, int version) {
        this(context, name, null, version);
    }

    private DBHelper(Context context, String name, SQLiteDatabase.CursorFactory factory, int version) {
        this(context, name, factory, version, null);
    }

    private DBHelper(Context context, String name, SQLiteDatabase.CursorFactory factory, int version, DatabaseErrorHandler errorHandler) {
        super(context, name, factory, version, errorHandler);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {

    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

    }


    /**
     * 判断某张表是否存在
     *
     * @param tabName 表名
     * @return
     */
    public boolean tabIsExist(String tabName) {
        boolean result = false;
        if (tabName == null) {
            return false;
        }
        SQLiteDatabase db = null;
        Cursor cursor = null;
        try {
            db = this.getReadableDatabase();//此this是继承SQLiteOpenHelper类得到的
            String sql = "select count(*) as c from sqlite_master where type ='table' and name ='" + tabName.trim() + "' ";
            cursor = db.rawQuery(sql, null);
            if (cursor.moveToNext()) {
                int count = cursor.getInt(0);
                if (count > 0) {
                    result = true;
                }
            }

        } catch (Exception e) {
            // TODO: handle exception
        }
        return result;
    }
}

```

