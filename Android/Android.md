#  Android



## 第一章

### *体系结构

1. 应用程序层
2. 应用程序框架层
3. 系统运行库层
4. Linux核心层

### *系统运行库包括的库

1. 程序库
2. Android运行时库

### 开发模式

1. 原生开发
2. 混合开发

### *项目结构

1. **AndroidManifest.xml：**

   * **项目的配置信息文件**

   * **声明应用程序的组件（activity，service，broadcast receiver，content provider）**

   * **设置权限和一些相关信息**

   * **是整个应用程序的入口**

2. Java：**放置源代码和测试代码**

3. res：资源目录，储存所有项目资源
   * layout：**存放xml布局文件**
   * values：**存放app应引用的一些值，子目录存放参数描述文件资源**
   * drawable：**存放图片资源**
   * anim：存放xml格式的动画资源
   * mipmap：**存放系统图片**
   * raw：存放任意文件，会被编译，R类中会生成id
   * assets：可以存放任意文件，不会被编译

4. r\debug：自动产生一个R.java文件，将res中的资源与id编号进行映射

### *Android应用程序结构

表现层与逻辑控制层分离

逻辑控制层由**java应用程序**实现，表现层由**XML文档**描述。

基本代码：

```java
public class MainAndroid extends Acitivity {
  public void onCreate() {
    super.onCreate(Bundle savedInstanceState);
    setContentView(R.layout, activity_main);
  }
}
```



## 第二章

### *View类

**View是用户界面组件的共同父类。**

**对于View类及其子类的属性，可以在布局文件XML中设置，也可以通过成员方法在java代码文件中动态设置。**

**共有属性3个：**

android:id

android:layout_width = “fill_parent” // 屏幕的宽度

android:layout_height = "wrap_content"

几个组件：

1. TextView

2. Button

3. EditView

### 布局

#### *总结

**LinearLayout**

**GridLayout**

**TableLayout**

**FrameLayout**

**RelativeLayout**

wrap_content：根据组件内容的大小来决定组件

match_parent：使组件填充所在容器的所有空间

px：像素

**dp：设备独立像素，抽象单位，与屏幕大小无关**

**sp：比例像素，设置字体大小**

android:gravity：控制组件对齐方式

#### 线性布局

android:orientatiion = "horizontal" / "vertical"

#### 表格布局

```xml
<TableRow></TableRow> // 定义行
android:shrinkColumns // 定义列
```

#### 网格布局

```xml
// 用于<GridLayout></GridLayout>的属性
android:columnCount // 定义列的数量
android:rowCount    // 定义行的数量
// 用于子元素的属性
android:layout_columnSpan  // 组件占据的列数
android:layout_rowSpan     // 组件占据的行数
```

#### 帧布局

左上角，组建会被遮盖

#### 相对布局

相对其他组件的位置的布局方式

### CheckBox和RadioGroup

ischecked()

getText()

### ImageView

android:src  

setImageResource(src)

```java
public class MainAndroid extends Acitivity {

  private int[] imgs = {
    R.drawable.img1,
    R.drawable.img2
  };

  public void onCreate() {
    super.onCreate(Bundle savedInstanceState);
    setContentView(R.layout, activity_main);

    image = (ImageView)findViewById(R.id.ImageView);
    image.setImageResource(imgs[0]);
  }
}
```

### Toast

```java
Toast toast

toast = Toast.makeText(getApplicantionContext(), "已下载", Toast.LENGTH_SHORT);
toast.setGravity(Gravity.CENTER, 0, 0);
toast.show();
```

### *ListView

```java
public class MainActivity extends AppCompatActivity {

    private String[] data = {
        "Apple",
        "Banana",
        "Orange",
        "Watermelon",
        "Pear"
    };

    ListView listView; // 数据

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        listView = (ListView)findViewById(R.id.ListView1);

        // 定义数组适配器
        ArrayAdapter<String> adapter = new ArrayAdapter<String>(
                MainActivity.this,            // Context上下文
                android.R.layout.simple_list_item_1,  // 子项布局id
                this.data);

        // 为数组设置适配器
        listView.setAdapter(adapter);

       int[] headerID = {
            R.drawable.logo,
            R.drawable.logo2,
            R.drawable.logo,
            R.drawable.logo2,
            R.drawable.logo
        };

        List<Map<String, Object>> listTest = new ArrayList<Map<String, Object>>();

        for(int i = 0; i < data.length; i++){
            Map<String, Object> listItem = new HashMap<String, Object>();
            listItem.put("header", headerID[i]);
            listItem.put("name", data[i]);
            listTest.add(listItem);
        }

        SimpleAdapter simpleAdapter = new SimpleAdapter(
            this,                         //上下文
            listTest,                     //数据源，包含map的List
            R.layout.list_array,          //自定义的列表项的布局文件
            new String[] {"header", "name"},
            new int[] {R.id.header, R.id.name});

        listView.setAdapter(simpleAdapter);

        listView.setOnItemClickListener(new mItemClick());
    }

    class mItemClick implements AdapterView.OnItemClickListener {

        AlertDialog.Builder dialog = new AlertDialog.Builder(MainActivity.this);

        @Override
        public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
            dialog.setTitle("您选择的水果");
            dialog.setMessage(data[position]);
            dialog.setPositiveButton("确定", new okClick());
            dialog.create();
            dialog.show();
        }
    }

    class okClick implements DialogInterface.OnClickListener {

        @Override
        public void onClick(DialogInterface dialog, int which) {
            dialog.cancel();
        }
    }
}

```



## 第三章

### *Intent对象使用场合

1. 页面切换
2. 传递数据
3. 调用外部程序

### *页面的切换

```java
Ietent intent = new intent(MainActivity.this, Second.this);
startActivity(intent);
```

### *传递数据

```java
// A的操作
Intent intent = new Intent();
Bundle bundle = new Bundle();

intent.setClass(MainActivity.this, Second.this);
bundle.putString("text", txt.getText().toString());
intent.putExtras(bundle);
startActivity(intent);

// B操作
Bundle bundle = this.getIntent().getExtras();
bundle.getString("text");
```

### 菜单设计

#### *分类

1. 选项菜单
2. 上下文菜单
3. 子菜单

#### 选项菜单

```java
// 在MainActivity里重写此方法
@Override
public boolean onCreateOptionsMenu(Menu menu) {
	super.onCreateOptionMenu(menu);
	menu.add(
		1,        // 组号
		1，       // 唯一的id号
		1，       // 排序号
		"菜单项1"，// 标题
	)
	return true;
}
// 处理每一项的内容
@Override
public boolean onOptionsItemSelected(MenuItem item) {
	switch(item.getItemId()) {
		// 响应每个菜单项，通过id
		case 1:
			...
			break;
		case 2:
			...
			break;
		default:
			return super.onOptionsItemSelected(item);
	}
    return true;
} 
```

#### 上下文菜单

```java
// 在onCreate里面注册
public void onCreate(Bundle savedInstanceState) {
	super.onCreate(savedInstanceState);
	setContentView(R.layout.activity_main)
	
	txt = (TextView)findViewById(R.id.textView1);
	
	registerForContextMenu(txt);
}

// 重写方法
public void onCreateContextMenu(ContextMenu menu, View  view, ContextMenuInfo) {
    menu.serHHeaderTitle("example");
    menu.add(1, item, 1, "asdasd");
}
// 处理每一项
public boolean onContextItemSelected(MenuItem item) {
    switch(item.getItemId()) {
        case item1: 
            ...
            break;
    }
    return true;
}
```

### 对话框

```java
Builder dialog = new AlertDialog.Builder(MainActivity.this);
public void onClick(view v) {
    dialog.setTitle("s");
    dialog.setMessage("sdsd");
    dialog.setPositiveButton("sd", new okClick());
    dialog.setNegativeButton("sd", new exitClick());
    dialog.create();
    dialog.show();
}

Class okClick implements DialogInterface.OnclickListener{
    @Override
    public void onClick(DialogInterface dialog) {
        dialog.cancel(); // 和dialog.dismiss没有区别
    }
}
```



## 第五章

### *弄清楚service的运行流程

**一个服务只能创建一次，销毁一次，但是可以开始多次。**

点击启动 -> onCreate() -> onStartCommand() -> 点击启动 -> onStartCommand() -> 点击终止 -> onDestroy()

### *设计后台服务应用程序的步骤

1. **创建Service的子类**

   编写onCreate()方法，创建后台服务；

   编写onStartCommand()方法，启动后台服务；

   编写onDestroy()方法，终止后台服务，并删除所有调用。

2. **创建启动和控制Service的Activity：**
  
   创建Intent对象，建立Activity与Service的关联；

   调用Activity的 startService(Intent) 方法启动Service后台服务；
   
   调用Activity的 stopService(Intent) 方法关闭Service后台服务。

3. **修改配置文件AndroidManifest.xml：**
  
   在配置文件AndroidManifest.xml的<application>标签中添加如下代码：

```
<service android:enabled="true" android:name=".AudioSrv" /> 
```

### *后台服务

```java
// 服务类
public class Server extends Service {
	public IBinder onBind(Intent intent) {
        return null;
    }
    public void onCreate() {
        super.onCreate();
    }
    public int onStartCommand(Intent intent, int flags, int startId) {
        super onStartCommand(intent, flags, startId);
        return START_STICKY; // 常量，表示如果进程被杀死，立即重启，保持启动状态，不保留intent
    }
    public void onDestroy() {
        super.onDestroy();
    }
}

// MainActivity
intent = new Intent(MainActivity.this, Server.class);
MainActivity.this.startService(intent);
MainActivity.this.stopService(intent);
```

### *广播

什么是广播？什么是广播接受者？

**Broadcast是Android系统应用程序之间传递信息的一种机制。**

**BroadcastReceiver是用来接收来自系统和应用中的广播信息的组件。**

系统之间需要传递某些信息，不是通过诸如单击按钮之类的组件来触发，而是由系统自身通过系统调用来引发事件，把这种由BraodcastReceiver类实现的系统调用称为广播。

### *注册广播

**静态注册：**在androidManifest.xml注册

```xml
<service android:name=".TestReceiver">
   <intent-filter> 
	  <action android:name="abc" />
   </intent-filter>  
</service > 
```

**动态注册：**onCreate()里面

```java
BordercastReceiver receiver = new BordercastReceiver();
IntentFilter filter = new IntentFilter();
filter.addAction("包名")；
registerReceiver(receiver. filter);
```

### !!广播输出当前时间

**动态注册获取系统时间**

```java
// onCreate
BordercastReceiver receiver = new BordercastReceiver();
IntentFilter filter=new IntentFilter();
filter.addAction(Intent.ACTION_TIME_TICK);
registerReceiver(receiver,filter);

// 静态注册
Intent intent = new Intent();
bundle.putString("time", Intent.ACTION_TIME_TICK);
intent.putExtras(bundle);
intent.setAction("abc");
sendBroadcast(intent);

// onDeStroy()
protected void onDestroy() {
    super.onDestroy();
    unregisterReceiver(receiver);
}
```

**接收广播**

```java
public class TestReceiver extends BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {
      String action = intent.getAction();
      if (action.equals(Intent.ACTION_TIME_TICK)) {

      }
    }
}
```



## 第六章

### *加载URL网站页面

```java
webView.loadUrl(“ 网页地址”)
```



### JavaScript 调用 Java 的方法：

webView（java）调用js的基本格式为：webView.loadUrl(“javascript:方法名(参数)”)

JavaScript调用Java：window.jsInterfaceName.方法名(参数) 

在Android 4.2之前可以使用 addjavascriptinterface 的方式注入原生的Java中,给JavaScript调用。

在4.2之后Android提供了**@JavascriptInterface对象注解的方式建立Javascript对象和android原生对象的绑定**，提供给javascript调用的函数必须带有@JavascriptInterface。



### *Socket的主要方法

```java
getInputStream()  // 获得一个输入流，读取从网络线路上传送来的数据信息。
getOutputStream() // 获得一个输出流，用这个输入流将数据信息写入到网络"线路”上。
```



### **客户端给服务器发数据

```java
public void client() {
	try {
		Socket socket = new Socket("192.168.0.1", 4321);
    } catch (Exception ioe) {
        
    }

    try {
        dis = new DataInputStream(socket.getInputStream());
        dos = new DataOutputStream(socket.getOutputStream());
        dos.writeUTF("....");
        dos.flush();
    } catch (Exception ioe) {
        
    }

	try {
        Thread.sleep(500);
        msg = "...";
        WriteString(msg);

        dis.close();
        socket.close();
    } catch (Exception ioe) {
        
    }

}

public void WriteString(String str) {
	dos.writeUTF(str);
	dos.flush();
	socket.close();
}
```

### *获取httpURLConnection的对象

调用url的openConnection()方法

```java
conn = (HttpURLConnection)url.openConnection();
```

### !!获取URL下载并保存到指定目录

基本流程
当我们想要下载网站上的某个资源时，我们会获取一个url，它是服务器定位资源的一个描述，下载的过程有如下几步：
**（1）客户端发起一个url请求，获取连接对象。**
**（2）服务器解析url，并且将指定的资源返回一个输入流给客户。**
**（3）建立存储的目录以及保存的文件名。**
**（4）输出了写数据。**
**（5）关闭输入流和输出流。**

```java
/**  
 * @从制定URL下载文件并保存到指定目录
 * @param filePath 文件将要保存的目录  
 * @param method 请求方法，包括POST和GET  
 * @param url 请求的路径  
 * @return  
 */  
  
public static File saveUrlAs(String url,String filePath,String method){  
     //System.out.println("fileName---->"+filePath);  
     //创建不同的文件夹目录  
     File file=new File(filePath);  
     //判断文件夹是否存在  
     if (!file.exists())  
     {  
        //如果文件夹不存在，则创建新的的文件夹  
         file.mkdirs();  
     }  
     FileOutputStream fileOut = null;  
     HttpURLConnection conn = null;  
     InputStream inputStream = null;  
     try  
     {  
         // 建立链接  
         URL httpUrl=new URL(url);  
         conn=(HttpURLConnection) httpUrl.openConnection();  
         //以Post方式提交表单，默认get方式  
         conn.setRequestMethod(method);  
         conn.setDoInput(true);    
         conn.setDoOutput(true);  
         // post方式不能使用缓存   
         conn.setUseCaches(false);  
         //连接指定的资源   
         conn.connect();  
         //获取网络输入流  
         inputStream=conn.getInputStream();  
         BufferedInputStream bis = new BufferedInputStream(inputStream);  
         //判断文件的保存路径后面是否以/结尾  
         if (!filePath.endsWith("/")) {  
             filePath += "/";   
         }  
         //写入到文件（注意文件保存路径的后面一定要加上文件的名称）  
         fileOut = new FileOutputStream(filePath+"123.png");  
         BufferedOutputStream bos = new BufferedOutputStream(fileOut);  
           
         byte[] buf = new byte[4096];  
         int length = bis.read(buf);  
         //保存文件  
         while(length != -1)  
         {  
             bos.write(buf, 0, length);  
             length = bis.read(buf);  
         }  
         bos.close();  
         bis.close();  
         conn.disconnect();  
    } catch (Exception e)  
    {  
         e.printStackTrace();  
         System.out.println("抛出异常！！");  
    }  
       
     return file;  
       
 }  
  
// 测试类
  
/**  
 * @param args  
 */  
public static void main(String[] args)  
{  
    String photoUrl = "123.png";   //文件URL地址                                     
    String fileName = photoUrl.substring(photoUrl.lastIndexOf("/"));     //为下载的文件命名
    String filePath = "d:";      //保存目录
    File file = saveUrlAs(photoUrl, filePath + fileName,"GET");    
}
```



## 第八章

### *shell命令

```java
abd shell          // 进入控制台
sqlite3 数据库名.db // 访问数据库
```

### *创造数据库的方法

1. 创建数据库的方法有多种，可以应用SQLiteDatabase对象openDatabase()方法及openOrCreateDatabase（）方法创建数据库；

2. 可以应用SQLiteOpenHelper的子类创建数据库；

3. 还可以应用Activity继承于父类android.content.Context创建数据库的方法openOrCreateDatabase（）来创建数据库。

### *获取SQLlite的方法

```java
GetWritableDatabase() // 以读写方式创建或打开数据库
GetReadableDatabase() // 创建或打开数据库
```

### !!数据库

```java
// MainActivity.java
public class MainActivity extends AppCompatActivity {

    static EditText editText1, editText2, editText3, editText4;
    Button prev, next, open, close, add, review, delete;
    Cursor cursor;
    // SQLiteDatabase db;
    DBHelper helper;
    public int id_this;
    Bundle savedInstanceState;

    // Users（_id（不是id）,username, usertel, useraddress, useremail）
    static String TABLE_NAME = "Users";
    static String ID = "_id";
    static String username = "username";
    static String usertel = "usertel";
    static String useraddress = "useraddress";
    static String useremail = "useremail";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editText1 = (EditText)findViewById(R.id.editText1);
        editText2 = (EditText)findViewById(R.id.editText2);
        editText3 = (EditText)findViewById(R.id.editText3);
        editText4 = (EditText)findViewById(R.id.editText4);

        open = (Button)findViewById(R.id.open);
        open.setOnClickListener(new myClick());

        close = (Button)findViewById(R.id.close);
        close.setOnClickListener(new myClick());

        prev = (Button)findViewById(R.id.prev);
        prev.setOnClickListener(new myClick());

        next = (Button)findViewById(R.id.next);
        next.setOnClickListener(new myClick());

        add = (Button)findViewById(R.id.add);
        add.setOnClickListener(new myClick());

        review = (Button)findViewById(R.id.review);
        review.setOnClickListener(new myClick());

        delete = (Button)findViewById(R.id.delete);
        delete.setOnClickListener(new myClick());
    }

class myClick implements View.OnClickListener {
    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.open:
                // 建立数据库
                helper = new DBHelper(MainActivity.this);
                SQLiteDatabase db = helper.getWritableDatabase();
                // 打开数据库
                db = openOrCreateDatabase("PhoneBook.db", Context.MODE_PRIVATE, null);
                cursor = db.query("Users", null, null, null, null, null, null);
                cursor.moveToNext();
                prev.setClickable(true);
                next.setClickable(true);
                review.setClickable(true);
                delete.setClickable(true);
                break;
            case R.id.close:
                cursor.close();
                editText1.setText("数据库已关闭");
                editText2.setText("数据库已关闭");
                editText3.setText("数据库已关闭");
                editText4.setText("数据库已关闭");
                prev.setClickable(false);
                next.setClickable(false);
                review.setClickable(false);
                delete.setClickable(false);
                break;
            case R.id.prev:
                if(!cursor.isFirst()) {
                    cursor.moveToPrevious();
                }
                dataShow();
                break;
            case R.id.next:
                if(!cursor.isLast()) {
                    cursor.moveToNext();
                }
                dataShow();
                break;
            case R.id.add:
                add();
                break;
            case R.id.review:
                review();
                break;
            case R.id.delete:
                delete();
                break;
        }

    }
        void dataShow() {
            id_this = Integer.parseInt(cursor.getString(0));
            String user_name_this = cursor.getString(1);
            String telephone_this = cursor.getString(2);
            String address_this = cursor.getString(3);
            String mail_this = cursor.getString(4);
            editText1.setText(user_name_this);
            editText2.setText(telephone_this);
            editText3.setText(address_this);
            editText4.setText(mail_this);
        }

        void add() {
            ContentValues values = new ContentValues();
            values.put(username, MainActivity.editText1.getText().toString());
            values.put(usertel, MainActivity.editText2.getText().toString());
            values.put(useraddress, MainActivity.editText3.getText().toString());
            values.put(useremail, MainActivity.editText4.getText().toString());

            String where1 = ID + " = " + id_this;
            SQLiteDatabase db = helper.getWritableDatabase();
            db.insert(TABLE_NAME, null, values);
            db.close();
        }

        void review() {
            ContentValues values = new ContentValues();
            values.put(username, MainActivity.editText1.getText().toString());
            values.put(usertel, MainActivity.editText2.getText().toString());
            values.put(useraddress, MainActivity.editText3.getText().toString());
            values.put(useremail, MainActivity.editText4.getText().toString());

            String where1 = ID + " = " + id_this;
            SQLiteDatabase db = helper.getWritableDatabase();
            db.update(TABLE_NAME, values, where1, null);
            db.close();
        }

        void delete() {
            String where = ID + " = " + id_this;
            SQLiteDatabase db = helper.getWritableDatabase();
            db.delete(TABLE_NAME, where, null);
            db.close();
        }
    }
}

// DBHepler
public class DBHelper extends SQLiteOpenHelper {

    static final String Database_name = "PhoneBook.db";
    static final int Database_Version = 1;
    SQLiteDatabase db;
    public int id_this;
    Cursor cursor;

    // Users（_id（不是id）,username, usertel, useraddress, useremail）
    String TABLE_NAME = "Users";
    String ID = "_id";
    String username = "username";
    String usertel = "usertel";
    String useraddress = "useraddress";
    String useremail = "useremail";

    public DBHelper(Context context) {
        super(context, Database_name, null, Database_Version);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        String sql = "CREATE TABLE " + this.TABLE_NAME + " ("
                + this.ID + " INTEGER PRIMARY KEY autoincrement, "
                + this.username + " text not null, "
                + this.usertel + " text not null, "
                + this.useraddress + " text not null, "
                + this.useremail + " text not null " + ");" ;
        db.execSQL(sql);
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

    }
}


```



### *对SD卡进行读写用到的类

环境变量访问类：environment

及其两个方法：

```java
getExternalStorageState() // 获取当前存储设备的状态

getExternalStorageDirectory() // 获取SD卡的根目录
```

### *描述数据存储的过程

1. 使用 Activity 类的 getSharedPreferences 方法获取到 SharedPreferences 对象，指定文件名和访问权限 

2. 获得 SharedPreferences.Editor 对象，并使用该对象的 putXxx方法 保存key-value对。

3. 通过 SharedPreferences.Editor 的 commit 方法保存（提交）key-value键值对。

```java
// 获取
SharedPreferences setting = getSharedPreferences("phoneBook", Context.MODE_PRIVATE);
SharedPreferences.Edit edit = setting.edit();
edit.getString("ssd");
edit.remove("sdsd");
edit.clear();

// 存储
SharedPreferences setting = getSharedPreferences("phoneBook", Context.MODE_PRIVATE);
SharedPreferences.Edit edit = setting.edit();
edit.putString("sds", "sddsd");
editor.commit();
```

