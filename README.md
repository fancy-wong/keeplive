# KeepLive for Android 安卓保活组件
## 集成了无声音乐（已考虑功耗，降至最低），前台服务、双进程守护、像素保活，jobs五种保活方式
## 主流的魅族、小米、锤子、vivo、努比亚、三星、华为等品牌，涵盖4.4至9.0的机型测试结果为，只要用户不主动杀死程序就不会死，但某些机型锁屏即断网的问题不是我能解决的。
## 更新日志
### 【1.1.5 】 2019-01-25 
#### 1.简化了集成流程，无需再配置manifest文件；
### 【1.1.4 】 2019-01-24 
#### 1.修复了unbindService(connection)可能造成部分机器java.lang.IllegalArgumentException: Service not registered的bug；
### 【1.1.3 】 2019-01-07 
#### 1.修复了jobservice中获取remote进程存活状态永远为false的bug；
### 【1.1.2 】 2019-01-02 
#### 1.修复了应用切换到后台息屏再亮屏，应用会自动显示到前台的bug；
### 【1.1.1 】 2018-12-28 
#### 1.应@bob要求，不再要求对KeepLive.startWork()方法中ForegroundNotification强制传参，如果不想要前台服务则传null就可以了。经过极端压力测试，在不使用前台服务的情况下，扛不住，所以不建议不使用前台服务；
### 【1.1.0 稳定版】 2018-12-25 【注意看集成文档，本次更新了一些配置】
#### 1.新增安卓7.0及以下自动隐藏通知特性
#### 2.消除安卓9.0会有通知声音的问题
### 【1.0.8】 2018-12-11
#### 1.修改ENERGY省电模式保活逻辑，保活效果更好一些，不过肯定不如ROGUE（流氓模式）
#### 2.修改KeepLiveService的实现方法，不再传递Context
### 【1.0.7】 2018-12-05 
#### 1.新增RunMode（运行模式）设定，可设置ENERGY（省电模式）、ROGUE（流氓模式），多数情况下建议使用省电模式，经测试即时是省电模式，保活效果依然很强悍
### 【1.0.6】 2018-11-30 
#### 1.适配安卓8.0以上，修正startForegroundService引起not found service进而造成某些机型NAR的问题
### 【1.0.4】 2018-11-15 
#### 1.修改OnePixelActivity的基类为Activity，避免由于主题造成兼容问题
#### 2.适配安卓8.0以上，将安卓8.0以上的startservice改为startForegroundService，增强了稳定性
### 【1.0.3】 2018-10-25 
#### 1.修复了在安卓9.0版本上引发闪退的bug
#### 2.ForegroundNotificationClickListener新增Context参数，用于通知栏传递值
### 使用方式，在application中启动保活服务
```Java
        //定义前台服务的默认样式。即标题、描述和图标
        ForegroundNotification foregroundNotification = new ForegroundNotification("测试","描述", R.mipmap.ic_launcher,
                //定义前台服务的通知点击事件
                new ForegroundNotificationClickListener() {
                    
                    @Override
                    public void foregroundNotificationClick(Context context, Intent intent) {
                    }
                });
        //启动保活服务
        KeepLive.startWork(this, KeepLive.RunMode.ENERGY, foregroundNotification,
                //你需要保活的服务，如socket连接、定时任务等，建议不用匿名内部类的方式在这里写
                new KeepLiveService() {
                    /**
                     * 运行中
                     * 由于服务可能会多次自动启动，该方法可能重复调用
                     */
                    @Override
                    public void onWorking() {

                    }
                    /**
                     * 服务终止
                     * 由于服务可能会被多次终止，该方法可能重复调用，需同onWorking配套使用，如注册和注销broadcast
                     */
                    @Override
                    public void onStop() {
                        
                    }
                }
        );
```
### 依赖
#### Maven
```Xml
<dependency>
  <groupId>com.fanjun</groupId>
  <artifactId>keeplive</artifactId>
  <version>1.1.5</version>
  <type>pom</type>
</dependency>
```
#### Gradle
```Xml
implementation 'com.fanjun:keeplive:1.1.5'
```

#### 联系我
```Xml
我的博客：https://blog.csdn.net/qwe112113215
```
```Xml
我的邮箱：810343451@qq.com
```
