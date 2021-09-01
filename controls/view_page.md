# ViewPage

## 介绍

ViewPager就是一个简单的页面切换组件，我们可以往里面填充多个View，然后我们可以左 右滑动，从而切换不同的View，我们可以通过`setPageTransformer()`方法为我们的ViewPager 设置切换时的动画效果，和前面学的ListView，GridView一样，我们也需要一个Adapter (适配器)将我们的View和ViewPager进行绑定，而ViewPager则有一个特定的Adapter——* **PagerAdapter***！另外，Google官方是建议我们使用Fragment来填充ViewPager的，这样 可以更加方便的生成每个Page，以及管理每个Page的生命周期！给我们提供了两个Fragment 专用的Adapter：***FragmentPageAdapter***和***FragmentStatePagerAdapter** *我们简要的来分析下这两个Adapter的区别：

- **FragmentPageAdapter**：和PagerAdapter一样，只会缓存当前的Fragment以及左边一个，右边 一个，即总共会缓存3个Fragment而已，假如有1，2，3，4四个页面：
  处于1页面：缓存1，2
  处于2页面：缓存1，2，3
  处于3页面：销毁1页面，缓存2，3，4
  处于4页面：销毁2页面，缓存3，4
  更多页面的情况，依次类推~

- **FragmentStatePagerAdapter**：当Fragment对用户不 见得时，整个Fragment会被销毁， 只会保存Fragment的状态！而在页面需要重新显示的时候，会生成新的页面！

**总结；**

FragmentPageAdapter适合固定的页面较少的场合；而FragmentStatePagerAdapter则适合 于页面较多或者页面内容非常复杂(需占用大量内存)的情况！*

## PageAdapter

最普通的PagerAdapter，如果想使用这个PagerAdapter需要重写下面的四个方法： 当然，这只是官方建议，实际上我们只需重写`getCount()`和`isViewFromObject()`就可以了~

- **getCount()**:获得viewpager中有多少个view
- **destroyItem()**:移除一个给定位置的页面。适配器有责任从容器中删除这个视图。 这是为了确保在finishUpdate(viewGroup)返回时视图能够被移除。

而另外两个方法则是涉及到一个key的东东：

- **instantiateItem()**: ①将给定位置的view添加到ViewGroup(容器)中,创建并显示出来 ②返回一个代表新增页面的Object(key),通常都是直接返回view本身就可以了,当然你也可以 自定义自己的key,但是key和每个view要一一对应的关系
- **isViewFromObject()**: 判断`instantiateItem(ViewGroup, int)`函数所返回来的Key与一个页面视图是否是 代表的同一个视图(即它俩是否是对应的，对应的表示同一个View),通常我们直接写 return view == object!



![img](view_page-images/68392114.jpg)

1. 首先创建View布局 **view_one.xml** 其余两个一致、

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
           android:layout_width="match_parent"
           android:layout_height="match_parent"
           android:background="#ffcc"
           >
       <TextView
               android:layout_width="wrap_content"
               android:layout_height="wrap_content"
               android:text="页面一"
               />
   
   </FrameLayout>
   ```

   

2. 创建一个类继承`PagerAdapter` 并实现其方法

   ```java
   package com.xuelingmiao.learncontrol.viewpage;
   
   import android.view.View;
   import android.view.ViewGroup;
   
   import androidx.annotation.NonNull;
   import androidx.viewpager.widget.PagerAdapter;
   
   import java.util.ArrayList;
   
   public class MyPageAdapter extends PagerAdapter {
       private ArrayList<View> viewList;
   
       public MyPageAdapter() {
       }
   
       public MyPageAdapter(ArrayList<View> viewList) {
           this.viewList = viewList;
       }
   
       //总view数
       @Override
       public int getCount() {
           return viewList.size();
   
       }
       // 将指定位置的view添加到容器中并显示出来，需要返回一个代表新镇页面的obj类型的key
       @NonNull
       @Override
       public Object instantiateItem(@NonNull ViewGroup container, int position) {
           container.addView(viewList.get(position));
           return viewList.get(position);
       }
   
       // 判断 instantiateItem(ViewGroup, int) 函数所返回来的Key与一个页面视图是否是 代表的同一个视图
       @Override
       public boolean isViewFromObject(@NonNull View view, @NonNull Object object) {
           return view == object;
       }
   
   // 从容器中删除给定位置的view
       @Override
       public void destroyItem(@NonNull ViewGroup container, int position, @NonNull Object object) {
           container.removeView(viewList.get(position));
       }
   }
   
   ```

   

3. 构建布局view并为viewPage设置Adapter

   ```java
   package com.xuelingmiao.learncontrol.viewpage;
   
   import androidx.appcompat.app.AppCompatActivity;
   import androidx.viewpager.widget.ViewPager;
   
   import android.os.Bundle;
   import android.view.LayoutInflater;
   import android.view.View;
   
   import com.xuelingmiao.learncontrol.R;
   
   import java.util.ArrayList;
   
   public class PageAdapterActivity extends AppCompatActivity {
   
       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_page_adapter);
   
           ViewPager viewPage = findViewById(R.id.view_page_adapter);
           //加载布局文件
           ArrayList<View> views = new ArrayList<>();
           LayoutInflater layoutInflater = getLayoutInflater();
           views.add(layoutInflater.inflate(R.layout.page_one,null,false));
           views.add(layoutInflater.inflate(R.layout.page_two,null,false));
           views.add(layoutInflater.inflate(R.layout.page_three,null,false));
           //构建被为viewPage设置适配器
           MyPageAdapter myPageAdapter = new MyPageAdapter(views);
           viewPage.setAdapter(myPageAdapter);
       }
   }
   ```
   
   





