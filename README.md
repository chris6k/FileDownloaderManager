FileDownloaderManager
=====================

FileDownloader library for android



### filedownload-samples: 

Sample to show how to use the lib   



### filedownload:
Lib


==================

### 组件的调用API

```java
public class FileDownloader{
  // 构造函数
  // context Context 实例，一般为一个 activity 实例
  // download_url 要下载的 URL
  // file_save_dir 下载后的文件保存的位置
  // thread_num  启动几个线程进行下载
  public FileDownloader(Context context, String download_url, File file_save_dir, int thread_num);

  // 获取要下载的文件的大小(单位为字节)
  public int get_file_size();

  // 获取要下载的文件的名字
  public String get_file_name();

  // 开始下载
  // ProgressUpdateListener 监听下载数量的变化，listener 需要运行在UI线程
  // 如果不需要监听可以设置为 null
  public void download(ProgressUpdateListener listener);

  interface ProgressUpdateListener {
    public void on_update(int downloaded_size);
  }

  // 设置通知栏信息的点击事件行为
  public void set_notification(Class activity_class, Bundle intent_extras);
}
```



AndroidManiFest 设置
```java
<service android:name="com.mindpin.android.filedownloader.DownloadService" />

<receiver
    android:name="com.mindpin.android.filedownloader.TargetWidget"
    android:label="TargetWidget" >
    <intent-filter>
        <action android:name="app.action.target_widget" />
    </intent-filter>

</receiver>
```

使用示例

```java
Context context = // 某个 activity 实例
String url = "http://www.baidu.com/img/bdlogo.gif";
File save_dir  = new File("/sd/files");
FileDownloader fd = new FileDownloader(context, url, save_dir, 2);

fd.download(new ProgressUpdateListener(){
  public void on_update(int downloaded_size){
    // 这个方法需要运行在UI线程
    // 比如这里增加逻辑:在主界面显示下载进度条
    // downloaded_size 单位是字节，表示已经下载了的字节数

  }
});

```

==========
