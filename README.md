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
