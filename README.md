# Android Activity与Fragmen实现沉浸式状态栏
### 配置
#### 在 Projeczt中build.gradle里面添加
     allprojects {
	  	repositories {
	  		...
		  	maven { url 'https://jitpack.io' }
	  	}
  	}
#### 在项目build.gradle里面添加依赖：
     dependencies {
	        implementation 'com.github.tangguna:immersion:1.0.1'
   	}
	
#### 在styles.xml中配置如下：
     <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
        <item name="windowNoTitle">true</item>
    </style>

#### 在AndroidManifest.xml设置Activity主题：
     android:theme="@style/AppTheme"
     
### 使用方式
#### Activity顶部为图片时，在Activity的onCreate()里面添加
     StateBar.setTranslucentForImageViewInFragment(this, null);
   
![图片加载失败](https://github.com/tangguna/immersion/blob/master/img/activity.jpg)
