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

#### 设置状态栏顶部颜色
     StateBar.setColor(this, Color.parseColor("#3C89FD"));
     
   
### 设置Fragment状态栏颜色
#### 在设置fragment状态栏颜色时，需要设置xml布局最外层为LinearLayout布局，并在顶部添加View设置状态栏颜色
    <?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    xmlns:app="http://schemas.android.com/apk/res-auto"
	    android:orientation="vertical"
	    android:id="@+id/one"
	    android:fitsSystemWindows="true"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent">
	    <View
		android:id="@+id/fillStatusBarView"
		android:layout_width="match_parent"
		android:layout_height="0dp"
		android:background="#53ae71" />
	    <LinearLayout
		android:fitsSystemWindows="true"
		android:background="@color/colorAccent"
		android:orientation="vertical"
		android:layout_width="match_parent"
		android:layout_height="wrap_content">
		<include layout="@layout/title_layout"/>
	    </LinearLayout>
	</LinearLayout>

#### 随后在需要使用的Fragment或者BaseFragmen中添加
      StateBar.setFragmentImmersion(Context context,int id,View view)
##### id:view的id号，例如fillStatusBarView
##### view:布局
    @Override
    public View onCreateView(LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fg, container, false);
        StateBar.setFragmentImmersion(getContext(),R.id.fillStatusBarView,view)
        unbinder = ButterKnife.bind(this, view);
        return view;
    }
