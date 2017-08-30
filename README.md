# xBsdiff-23
增量更新框架，感谢鸿翔大神的博客

引用：

maven {url "https://raw.githubusercontent.com/610968110/xBsdiff-23/master"}

compile 'com.maven-liboxin:xBsdiff-23:1.0'

在项目的build里添加：

ext {

    //版本需要23

    compileSdkVersion = 23
    
    buildToolsVersion = "25.0.0"
    
    minSdkVersion = 19
    
    targetSdkVersion = 19
    
    }
    
    
 app及model的build里添加：
    
 compileSdkVersion rootProject.ext.compileSdkVersion
 
 buildToolsVersion rootProject.ext.buildToolsVersion
    
 minSdkVersion rootProject.ext.minSdkVersion
 
 targetSdkVersion rootProject.ext.targetSdkVersion

1、添加权限： 

  uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"

  6.0及以上需要动态添加权限：BsPatch.checkWritePermission(this);
  
  
2、初始化：只能初始化一次   

  BsPatch.init();
  
  
3、旧apk包和.patch文件合成新apk包   

   final File destApk = new File(Environment.getExternalStorageDirectory(), "new.apk");  
   
   final File patch = new File(Environment.getExternalStorageDirectory(), "PATCH.patch");  
   
   File newApk = BsPatch.bspatch(this, destApk, patch);
   
   
4、安装新的apk   

   if (newApk.exists()) 
   
   BsPatch.install(this, newApk.getAbsolutePath());
