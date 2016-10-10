# psandroidmatdesnimpltabs

##2 Introduction
### Intro
Material Design Support Library
```
NavigationView
CoordinatorLayout
FloatingActionButton
SnackBar
Floating Labels for EditText
AppBarLayout
CollapsingToolbarLayout
TabLayout
```

```
ViewPagerAdapter
FragmentPagerAdapter
FragmentStatePageAdapter
```

##3 Understanding ViewPager
###1 Introduction to ViewPager
###2 Simple ViewPager: Preparing Data Modal and Layout Resources
activity_main.xml
```
<android.support.v4.view.ViewPager android:id="@+id/viewPager" android:layout_width="match_parent" android:layout_height="match_parent" />
```

create viewpager_item.xml
```
<FrameLayout>
<ImageView android:id="@+id/imageItem" android:layout_width="match_parent" android:layout_height="match_parent" android:scaleType="centerCrop" android:src="@drawable/image1"/>
<TextView android:id="@+id/textViewItem" android:layout_width="wrap_content" android:layout_height="wrap_content" android_layout_gravity="bottom|center_horizontal" android:layout_marginButtom="48dp" android:text="placeholder" android:textColor="@android:color/white" android:textSize="35sp"/>
</FrameLayout>
```
