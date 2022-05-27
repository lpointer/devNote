### 流程

- 1.注册

> B界面将类的信息，通过key-value的形式，注册到arouter中。

- 2.查询

> A界面将类信息与额外信息（传输参数、跳转动画等），通过key传递至arouter中，并查询对应需要跳转类的信息。

- 3.结合

> 将A界面类信息、参数与B界面的类信息进行封装结合。

- 4.跳转

> 将结合后的信息，使用startActivity实现跳转。



### 使用

#### 跳转界面不带参

- 发送跳转操作

```java
// 1. 普通跳转
ARouter.getInstance().build("/test/activity").navigation();
```

- 目标界面

```java
// 在支持路由的页面上添加注解(必选)
// 这里的路径需要注意的是至少需要有两级，/xx/xx
@Route(path = "/test/activity")
public class YourActivity extend Activity {
    ...
}
```

#### 跳转界面带参

- 发送跳转操作

```java
ARouter.getInstance().build("/test/1")
            .withLong("key1", 666L)
            .withString("key3", "888")
            .withSerializable("key4", new Test("Jack", "Rose"))
            .navigation();
```

- 目标界面

```java
@Route(path = "/test/1")
public class YourActivity extend Activity {
    //获取数据三种方式
    //1.通过Autowired注解表明key   &  需要在onCreate中调用ARouter.getInstance().inject(this);配合使用
    @Autowired(name = "key1")
    public long data;
    //2.通过Autowired注解 & 将key1作为属性的名称   &  需要在onCreate中调用ARouter.getInstance().inject(this);配合使用
    @Autowired()
    public long key1;
    //3.通过Bundle获取
    getIntent().getExtras().getLong("key1")
}
```

#### 跳转界面带参(传递Object)

- 定义解析Obeject的SerializationService

```java
/**
 * 处理传递参数中自定义的Object---》withObject
 */
@Route(path = "/custom/json")
public class JsonSerializationService implements SerializationService {
    Gson gson;
    @Override
    public <T> T json2Object(String input, Class<T> clazz) {
        return gson.fromJson(input,clazz);
    }
    @Override
    public String object2Json(Object instance) {
        return gson.toJson(instance);
    }
    @Override
    public <T> T parseObject(String input, Type clazz) {
        return gson.fromJson(input,clazz);
    }
    @Override
    public void init(Context context) {
        gson = new Gson();
    }
}
```

- 发送跳转操作

```java
ARouter.getInstance().build("/test/1")
            .withObejct("key4", new Test("Jack", "Rose"))
            .navigation();
```

- 目标界面

```java
@Route(path = "/test/1")
public class YourActivity extend Activity {
    ...
    SerializationService serializationService = ARouter.getInstance().navigation(SerializationService.class);
    serializationService.init(this);
    User obj = serializationService.parseObject(getIntent().getStringExtra("key4"), User.class);
}
```

#### Uri跳转

- 界面配置

```java
<activity android:name=".activity.SchameFilterActivity">
    <!-- Schame -->
    <intent-filter>
        <data
        android:host="m.aliyun.com"
        android:scheme="arouter"/>
        <action android:name="android.intent.action.VIEW"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <category android:name="android.intent.category.BROWSABLE"/>
    </intent-filter>
</activity>
```

- 发送跳转操作

```java
 Uri testUriMix = Uri.parse("arouter://m.aliyun.com/test/activity2");
                ARouter.getInstance().build(testUriMix)
                        .withString("key1", "value1")
                        .navigation();
```

- 目标界面

```java
@Route(path = "/test/activity2")
public class Test2Activity extends AppCompatActivity {
}
```

#### 跳转结果监听

```java
 ARouter.getInstance()
              .build("/test/activity2")
              .navigation(this, new NavCallback() {
                   @Override
                    public void onArrival(Postcard postcard) {
                     }
                     @Override
                     public void onInterrupt(Postcard postcard) {
                           Log.d("ARouter", "被拦截了");
                      }
                 });
```

#### 声明拦截器(拦截跳转过程，面向切面编程)



```java
// 比较经典的应用就是在跳转过程中处理登陆事件，这样就不需要在目标页重复做登陆检查
// 拦截器会在跳转之间执行，多个拦截器会按优先级顺序依次执行
@Interceptor(priority = 8, name = "测试用拦截器")
public class TestInterceptor implements IInterceptor {
    @Override
    public void process(Postcard postcard, InterceptorCallback callback) {
    ...
    callback.onContinue(postcard);  // 处理完成，交还控制权
    // callback.onInterrupt(new RuntimeException("我觉得有点异常"));      // 觉得有问题，中断路由流程
    // 以上两种至少需要调用其中一种，否则不会继续路由
    }
    @Override
    public void init(Context context) {
    // 拦截器的初始化，会在sdk初始化的时候调用该方法，仅会调用一次
    }
}
```

#### 为目标页面声明更多信息

```java
// 我们经常需要在目标页面中配置一些属性，比方说"是否需要登陆"之类的
// 可以通过 Route 注解中的 extras 属性进行扩展，这个属性是一个 int值，换句话说，单个int有4字节，也就是32位，可以配置32个开关
// 剩下的可以自行发挥，通过字节操作可以标识32个开关，通过开关标记目标页面的一些属性，在拦截器中可以拿到这个标记进行业务逻辑判断
@Route(path = "/test/activity", extras = Consts.XXXX)
```

#### 依赖注入解耦

- 注册需要依赖注入的对象

```java
@Route(path = "/provider/testP")
public class TestProvider implements IProvider {
    @Override
    public void init(Context context) {
    }
    public String test(){
       return ("Hello Provider!");
    }
}
```

- 获取对象 & 使用

```java
ARouter.getInstance().navigation(TestProvider.class).test();
```
