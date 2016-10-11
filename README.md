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
create new class CustomPageAdapter.java
```
import android.content.Context;
class CustomPagerAdapter extends PagerAdapter{
  private Context cotext;
  private List<DataModel> itemList;
  
  private LayoutInflater inflater;
  public CustomPagerAdapter(Context context, List<DataModel> itemList){
    this.context =context;
    this.itemList=itemList;
    inflater = (LayoutInflater)context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
  }
  
  @Override
  public int getCount(){
    //returns length of itemList
    return itemList.size();
  }
  
  @Override
  public boolean isViewFromObject(View view, Object object){
    //return false;
    return view==object
  }
  
  
  @Override
  public Object instantiateItem(ViewGroup container,int position){
    View itemView = inflater.inflate(R.layout.viewpager_item,container,false);
    ImageView imageView = (ImageView)itemView.findViewById(R.id.imageItem);
    TextView textView = (TextView)itemView.findViewById(R.id.textViewItem);
    
    DataModel dataModel = itemList.get(position);
    imageView.setImageResource(dataModel.imageId);
    textView.setText(dataModel.title);
    
    container.addView(itemView);
    return itemView;
    //super.instantiateItem(container,position);
  }
  
  @Override
  public void destroyItem(ViewGroup container,int position,Object object){
    
  }
}
```


MainActivity.java
```
protected void onCreate(Bundle savedInstanceState){
  List<DataModel> itemList = getDataList();
  ViewPager viewPager = (ViewPager)findViewById(R.id.viewPager);
  CustomPagerAdapter adapter = new CustomPagerAdapter(this,itemList);
  viewPager.setAdapter(adapter);
}
```

(Hence, the rule is)
```
ViewPager.setAdapter(PagerAdapter)
```


###4 Analysing PagerAdapter Methods Using Logcat
When app starts, it loads 2 views(current+next), when traverse into middle, it keeps 3 items, destroy (n-2) first, then add (n+1)  
in CustomPagerAdapter.java
```
public void destroyItem(ViewGroup container, int position,Object object){
  container.removeView(FrameLayout(object));
}
```



###6 Implementing FragmentPagerAdapter
app/CustomAdapter.java
```
public class CustomAdapter extends FragmentPagerAdapter{

  private final int ITEMS=6;
  public CustomAdapter(FragmentManager fm){
    super(fm);
  }
  
  @Override
  public int getCount(){
    return ITEMS;
  }
  
  @Override
  public Fragment getItem(int position){
    switch(position){
      case 0:
        return new FragmentOne();
      ...
      default:
        rerurn new FragmentOne();
    }
  }
}
```

MainActivity.java
```
public class MainActivity extends AppCompatActivity{
public void onCreateVi
  super.onCreate(savedInstanceState);
  setContentView(R.layout.activity_main);
  ViewPager viewPager = (ViewPager)findViewById(R.id.viewPager);
  CustomAdapter adapter = new CustomAdapter(getSupportFragmentManager());
  viewPager.setAdapter(adapter);
}
```

###7 Analysing FragmentPagerAdapter in Detail
CustomAdapter.java
```
@Override
public void destroyItem(ViewGroup container, int position,Object object){
  if(mTransaction==null){
    mTransaction=mFragmanager.beginTransaction();
  }
  mTransaction.detach((Fragment)object);
}
```














##4 Implementing Simple Material Tabs with TabLayout
###2 Initial Project Setup
activity_main.xml
```
<RelativeLayout ....
<android.support.v7.widget.Toolbar android:id="@+id/toolbar" android:layout_width="match_parent" android:layout_height="?attr/actionBarSize" android:background="?attr/colorPrimary" android:layout_alignParentTop="true"/>

<LinearLayout android:layout_width="match_parent" android:layout_height="wrap_content" android:layout_margin="10dp" android:layout_centerInParent="true" android:orientation="vertical">

<Button android:id="@+id/btnSimpleTabs"
```


res/values/styles.xml
```
<resources>
<style name="AppTheme" parent="Theme.AppCompat.NoActionBar">
<item name="colorPrimary">@color/colorPrimary</item>
<item name="colorPrimaryDark">@color/colorPrimaryDark</item>
<item name="colorAccent">@color/colorAccent</item>
</style>
</resources>
```
res/values/colors.xml
```
<?xml>
<resources>
<color name="colorPrimary">#aaa</color>
<color name="colorPrimaryDark">#aaa</color>
<color name="colorAccent">#aaa</color>
</resources>
```
build.gradle
```
dependencies{
  compile 'com.android.support.appcompat-v7:23.3.0'
  compile 'com.android.support:design:23.3.0'
}
```















##5 Implementing Scrollable and Custom Tabs
###2 Implementing Scrollable Tabs
create ScrollTabsAdapter.java
```
public class ScrollTabsAdapter extends FragmentPagerAdapter{
  private List<Fragment> fragmentList;
  private List<String> titleList;
  
  public ScrollTabsAdapter(FragmentManger fm, List<Fragment> fragmentList, Lista<String> titleList){
    super(fm);
    this.fragmentList = fragmentList;
    this.titleList=titleList;
  }
  
  @Override
  public int getCount(){
    return fragmentList.size();
  }
  @Override
  public Fragment getItem(int position){
    return fragmentList.get(position);
  }
  
  @Override
  public CharSequence getPageTitle(int position){
    return titleList.get(position);
  }

}
```

tabs/ScrollTabs
```
public class ScrollTabs extends AppCompatActivity{
  private List<Fragment> fragmentList = new ArrayList<>();
  private List<String> titleList = new ArrayList<>();
  
  private ViewPager viewPager;
  private ScrollTabsAdapter adapter;
  peivate TabLayout tabLayout;
  
  @Override
  protected void onCreate(@Nullable Bundle savedInstanceState){
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_scroll_tabs);
    
    initialize();
    prepareDataResource();
    adapter = new ScrollTabsAdapter(getSupportFragmentManager(),fragmentList,titleList);
    
    viewPager.setAdapter(adapter);
    tabLayout.setupWithViewPager(viewPager);
  }
  
}
```
res/layout/scroll_tabs.xml
```

```
(4:40)
