# Note1

## 创建活动

### 创建和加载布局

1. 首先打开项目的 app/src/main/res/layout目录

2. 然后创建一个 SecondActivity.xml文件

3. 然后打开项目的 app/src/main/java 目录

4. 创建一个 SecondActivity.java文件

5. 输入如下代码

```

public class SecondActivity extends Activity

{

	@Override	protected void onCreate(Bundle savedInstanceState)

	{

		super.onCreate(savedInstanceState);

		setContentView(R.layout.SecondActivity);

	}

	

}

```

> 可以看到这里调用 setContentView() 方法给当前活动加一个布局，而在方法中，我们一般会传入一个布局的id。项目中添加的任何资源都会放到 R 文件中生成一个对应的资源 id。因此我们刚才创建的 SecondActivity.xml 的布局 id 已经添加到 R 文件中。在代码中引用布局，只需要调用 R.layout.SecondActivity 就可以得到 SecondActivity 的 id，然后传入 setContentView() 方法即可。

### 在 AndroidManifest.xml 中注册

1. 打开 app/src/main/AndroidManifest.xml 代码如下:

````

<?xml version="1.0" encoding="utf-8"?>

<manifest xmlns:android="http://schemas.android.com/apk/res/android"

    package="com.mycompany.myapp24" >

    <application

        android:allowBackup="true"

        android:icon="@drawable/ic_launcher"

        android:label="@string/app_name"

        android:theme="@style/AppTheme"

		android:resizeableActivity = "true">

        <activity

            android:name=".MainActivity"

            android:label="@string/app_name" >

            <intent-filter>

                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />

            </intent-filter>

        </activity>

    </application>

</manifest>

````

> 活动的注册要放到 `<application>` 标签内，通过 ` <activity>` 注册活动。在 `<activity>` 标签中我们使用

 android:name 来指定具体注册哪一个活动，这里的 .Maintivity 是 com.mycompany.myapp24.Maintivity 的缩写，由于最外层的 `<manifest>` 标签通过了 package 指定了程序的包名是 com.mycompany.myapp24 ，所以可以省略。`<intent-filtetr>` 中的这 `<action android:name="android.intent.action.MAIN" /> 和<category android:name="android.intent.category.LAUNCHER" />` 两句声明表示 Maintivity 是这个项目的主活动，在手机上点击应用图标后，首先启动的就是这个活动

2. 我们注册 SecondActivity 这个活动

```

 <activity

        android:name=".SecondActivity" >

</activity>

```

3. 让 SecondActivity 成为主活动。

```

<?xml version="1.0" encoding="utf-8"?>

<manifest xmlns:android="http://schemas.android.com/apk/res/android"

    package="com.mycompany.myapp24" >

    <application

        android:allowBackup="true"

        android:icon="@drawable/ic_launcher"

        android:label="@string/app_name"

        android:theme="@style/AppTheme"

		android:resizeableActivity = "true">

        <activity

            android:name=".MainActivity"

            android:label="@string/app_name" >

		</activity>

      

        <activity

        android:name=".SecondActivity" >

         <intent-filter>

                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />

            </intent-filter>

        </activity>

    </application>

</manifest>

```

就是把 `<intent-filter>` 标签放到 .SecondActivity活动下

## Toast弹窗

1. 首先定义一个弹窗的触发点。可以直接写在活动的 onCreate() 方法中。

2. 这里我们用按钮，来触发。在 SecondActivity.xml 中创建一个按钮。

```

	<Button

		android:layout_width="wrap_content"

		android:layout_height="wrap_content"

		android:text="Button"

		android:id="@+id/Button_1"/>

```

3. 在 SecondActivity.java 中的 onCreate() 方法中，添加如下代码:

```

protected void onCreate(Bundle savedInstanceState)

	{

		super.onCreate(savedInstanceState);

		setContentView(R.layout.SecondActivity);

		Button button1 = (Button) findViewById(R.id.Button_1);

		button1.setOnClickListener(new View.OnClickListener(){

				@Override

				public void onClick(View p1)

				{

					Toast.makeText(SecondActivity.this,"哈哈",Toast.LENGTH_LONG).show();

					

				}

			});

	}

```

4. 在活动中，通过 findViewByld() 方法获取在布局文件中的自定义元素，这里我们传入 R.id.Button_1，来得到按钮的实例，这个值在 SecondActivity.xml 通过 android:id 属性来指定。findViewByld() 方法返回的是一个 View 对象，我们需要向下转型，将他转成 Button对象。得到按钮的实例之后，通过调用 setOnclickListenter() 方法为按钮注册一个监听器。点击按钮时，就会执行监听器中的 onClick() 方法。所以弹窗在 onClick() 方法中编写

5. Toast 代码如下:

```java

Toast.makeText(MainActivity.this,"Node1",Toast

.LENGTH_LONG).show();

    

```

> 通过静态方法 makeText() 创建一个 Toast 对象，然后调用 show() 将弹窗显示出来。makeText()需要传入三个参数，第一个参数是 Context，也就是 Toast 要求的上下文，由于活动本身就是一个 Context 对象，因此这里直接传入 MainAivity.this 即可。第二个参数是 Toast 显示的文本内容。第三个参数是 Toast 显示的时长。
