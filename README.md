# gradle-
问题汇总

1、界面显示优化（笔记本电脑问题，设置电脑字体后部分字体显示不全
未处理

2、sdk的代码重复（未删除com.ck的代码
已处理：删除com.ck代码，插件重新出了一份APPproject2

3、资源重复
xx反编译处理掉了重复的资源，
重复的gradle有自己的一套方式，全部跟换为aar就不会有问题（默认使用母包的

4、点下一步的时候有时候会卡死
未处理

5、金立的资源循环引用
1）<resources xmlns:tools="http://schemas.android.com/tools">
2）<style name="gn_account_MyDialog" parent="@android:Theme.Dialog" tools:ignore="ResourceCycle">

6、android studio需要本地有sdk资源
在APPproject local.properties 中配置sdk.dir=D\:\\git\\packagetool\\CkGames\\tool\\Android\\Sdk
此sdk.dir需要配置成自动设置
sdk只需要带最简单的即可，需要其他的会自动下载（当前加上打包工具 压缩后500M）

可以试试tools是不是可以去掉

7、重复资源的gradle有自己的一套方式，全部跟换为aar就不会有问题（默认使用母包的
现在是删除母包重复资源（手动


8.Unzipping C:\Users\
Spider.Li\.gradle\wrapper\dists\gradle-5.6.4-all\ankdp27end7byghfw1q2sw75f\gradle-5.6.4-all.zip to C:\Users\
Spider.Li\.gradle\wrapper\dists\gradle-5.6.4-all\ankdp27end7byghfw1q2sw75f
Exception in thread "main" java.util.zip.ZipException: error in opening zip file

gradle-5.6.4-all.zip 下载解压出错

解决办法：上传cdn，修改本地配置地址
gradle依赖修改为阿里云https://www.cnblogs.com/fanlumaster/p/13726561.html
修改为阿里云的还是会下载到一半

9.java 不是内部或者外部命令，也不是可运行的程序
发行dex2jar 里的d2j_invoke.bat文件，使用的java命令，需要修改为指定的目录

10.Manifest merger failed : Attribute data@scheme at AndroidManifest.xml requires a placeholder substitution but no value for <APPLOG_SCHEME> is provided.
编译千面渠道的工程的时候会出现
参考https://blog.csdn.net/weixin_40750371/article/details/93630375 
无效
增加
debug  {
    minifyEnabled false
    proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
    manifestPlaceholders = [ appid:"aaaaa" ,"APPLOG_SCHEME" :""]
}
可行

11.More than one file was found with OS independent path 'META-INF/DEPENDENCIES'
https://blog.csdn.net/kenjili/article/details/93859505
packagingOptions {
        exclude 'META-INF/DEPENDENCIES'
}

12、is not a sibling in the same RelativeLayout [NotSibling]
直接删除该行
https://stackoverflow.com/questions/25527973/is-not-a-sibling-in-the-same-relativelayout

13、All com.android.support libraries must use the exact same version specification (mixing versions can
根据log 加上如下
api 'com.android.support:appcompat-v7:28.0.0'
api 'com.android.support:animated-vector-drawable:28.0.0'
api 'com.android.support:exifinterface:28.0.0'
api 'com.android.support:support-media-compat:28.0.0'
api 'com.android.support:support-v4:28.0.0'

每个渠道不一样
14、应用宝的微信授权后无法登录
WXEntryActivity.java 编译WXEntryActivity.class后需要放到APPproject 对应的libs目录 下

15、多套SDK兼容
请检查com.wf.   con.ck  com.a.q
com/wf com/ck


16\ Go to the documentation to learn how to <a href="d.android.com/r/tools/classpath-sync-errors">Fix dependency resolution errors</a>

海外的Google跟Twitter一个内容有冲突

17、D8: Invoke-customs are only supported starting with Android O (--min-api 26)

compileOptions {
        sourceCompatibility 1.8
        targetCompatibility 1.8
    }

并且设置compileSdkVersion 29


18、Caused by: com.android.tools.r8.CompilationFailedException: Compilation fail

multiDexEnabled true 

删除本地的support-multidex.jar

19、Program type already present: com.szckhd.jwgly.azyw.BuildConfig

https://blog.csdn.net/qq_39359887/article/details/90172767

第一次试的时候不成功，clean之后再来貌似是可以的

温馨提示：千万不要让游戏的包名跟SDK的一样

20、<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" android:maxSdkVersion="18"/>
会导致分享失败；vungle （topon中的，有配置maxsdkversion，因为是aar的没找到）； 在工程上添加 tool replace可以解决

21、xx.application classnotfound
多dex问题
https://blog.csdn.net/qq_36282231/article/details/81026296
https://developer.android.com/studio/build/multidex?hl=zh-cn


22、Caused by: java.lang.OutOfMemoryError: GC overhead limit exceeded
dexOptions {
    javaMaxHeapSize "4g"
}

#开启线程守护，第一次编译时开线程，之后就不会再开了
org.gradle.daemon=true
#配置编译时的虚拟机大小
org.gradle.jvmargs=-Xmx2048m -XX:MaxPermSize=512m -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
#开启并行编译，相当于多条线程再走
org.gradle.parallel=true
#启用新的孵化模式
org.gradle.configureondemand=true

23、还存在的问题
https://docs.gradle.org/5.6.4/userguide/gradle_daemon.html.
gradle-5.6.4-all.zip 下载不了

Daemon will be stopped at the end of the build stopping after processing
File C:\Users\CK\.android\repositories.cfg could not be loaded.
IOException: 
https://dl.google.com/android/repository/addons_list-3.xml
java.io.IOException: Unable to tunnel through proxy. Proxy returns "HTTP/1.1 401 Unauthorized"
IOException: 
https://dl.google.com/android/repository/addons_list-2.xml
java.io.IOException: Unable to tunnel through proxy. Proxy returns "HTTP/1.1 401 Unauthorized"

24、ImportError: DLL load failed
代码都跑不起来
exe 也无法执行
pip install pyqt4 安装不了 下的whl文件，安装后也是打不开

https://www.microsoft.com/zh-cn/download/confirmation.aspx?id=48145
先安装Visual C++ Redistributable for Visual Studio 2015

25、删除class.jar中的指定文件失败（实际是重新生成class.jar失败
因为jar 不是可识别的命令，配置java环境变量即可 
C:\Program Files\Java\jdk1.8.0_241\bin
按理说放到tools也行，就是懒得去弄了

26、HTC出包有问题
this can lead to crashes when the resource is queried in a configuration that does not match this qualifier [MissingDefaultResource]

看游戏是横屏还是竖屏，如果是竖屏就把竖屏文件里layout-port的xml拷贝一份到默认的layout文件夹里

27、打包工具所用dex2jar是修改过源码的版本
gradle打包方式，报错 java.lang.RuntimeException: can not merge I and Z
报错原因，dex2jar转换dex为jar时，转换部分方法失败。参考帖子：http://lonelyzerg.xyz/?p=135   https://ivonhoe.github.io/2017/02/09/美团如何防dex2jar/
    
    以此，可引申出as插件实现防反编译（但仅仅针对dex2jar）。

    解决方案：获取dex2jar源码，修改TypeClass.java类的实现，修改如下：
    不能放图！！！修改方式在上面的帖子中有。
    重新在项目根目录执行 ./gradlew 进行编译。替换TypeClass.java类所在的 dex-ir 模块的jar包。然后打包运行正常。
    网上帖子 https://sourceforge.net/p/dex2jar/tickets/237/  提到了两种处理方式，目前使用的是第二种处理方式。
-后续，测试发现，dex2jar 2.1 版本已经修复了此问题，但是该项目好像已经不再维护了，自己拉github代码下来，编译升级。遇到问题，大把截图放不了，有需要找俊峰要。






