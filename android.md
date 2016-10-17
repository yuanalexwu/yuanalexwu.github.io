# TODO
- [ ] Activity
- [ ] Service
- [ ] Broadcast Receive http://blog.csdn.net/liuhe688/article/details/6955668
- [ ] Content Provider
- [ ] Intent


**Broadcast Receive**
2中注册方法
android.content.ContextWrapper
静态注册:
应用退出MyReceiver任然收到MY_BROADCAST的广播
```xml
<receiver android:name=".MyReceiver">  
  <intent-filter>  
    <action android:name="android.intent.action.MY_BROADCAST"/>  
    <category android:name="android.intent.category.DEFAULT" />  
  </intent-filter>  
</receiver> 
```

动态注册:
应用退出MyReceiver就销毁
```java
MyReceiver receiver = new MyReceiver();         
IntentFilter filter = new IntentFilter();  
filter.addAction("android.intent.action.MY_BROADCAST");  
registerReceiver(receiver, filter);
```
动态创建需要销毁Receiver <span style="color: red;font-size:.8em">?此方法放在何处调用?</span>
```java
@Override  
protected void onDestroy() {  
    super.onDestroy();  
    unregisterReceiver(receiver);  
} 
```

**发送广播**
```java
public void send(View view) {  
    Intent intent = new Intent("android.intent.action.MY_BROADCAST");  
    intent.putExtra("msg", "hello receiver.");  
    sendBroadcast(intent);  
}  
```
