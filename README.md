原文：https://github.com/PoplarTang/FancyListIndexer

# FancyListIndexer
A fantastic indexer for listview or gridview. It will bypass your finger when you touch the letters. Hope you enjoy it!

##Demo
![](http://7xnwgc.com1.z0.glb.clouddn.com/git_github_FancyListIndexer_Demo1.gif)

##Dependency
[pinyin4j](http://pinyin4j.sourceforge.net/)

##Procedure
![](http://7xnwgc.com1.z0.glb.clouddn.com/git_github_FancyListIndexer_Procedure1.png)



public class MainActivity extends Activity {


	private ExpandableListView lv_content;
	private PingyinAdapter<GoodMan> adapter;

	public final String[] NAMES = new String[] { "A","aa","a","aaa","aaaaaa","aba","宋江", "卢俊义", "吴用",
			"公孙胜", "关胜", "林冲", "秦明", "呼延灼", "花荣", "柴进", "李应", "朱仝", "鲁智深",
			"武松", "董平", "张清", "杨志", "徐宁", "索超", "戴宗", "刘唐", "李逵", "史进", "穆弘",
			"雷横", "李俊", "阮小二", "张横", "阮小五", " 张顺", "阮小七", "杨雄", "石秀", "解珍",
			" 解宝", "燕青", "朱武", "黄信", "孙立", "宣赞", "郝思文", "韩滔", "彭玘", "单廷珪",
			"魏定国", "萧让", "裴宣", "欧鹏", "邓飞", " 燕顺", "杨林", "凌振", "蒋敬", "吕方",
			"郭 盛", "安道全", "皇甫端", "王英", "扈三娘", "鲍旭", "樊瑞", "孔明", "孔亮", "项充",
			"李衮", "金大坚", "马麟", "童威", "童猛", "孟康", "侯健", "陈达", "杨春", "郑天寿",
			"陶宗旺", "宋清", "乐和", "龚旺", "丁得孙", "穆春", "曹正", "宋万", "杜迁", "薛永", "施恩",
			"周通", "李忠", "杜兴", "汤隆", "邹渊", "邹润", "朱富", "朱贵", "蔡福", "蔡庆", "李立",
			"李云", "焦挺", "石勇", "孙新", "顾大嫂", "张青", "孙二娘", " 王定六", "郁保四", "白胜",
			"时迁", "段景柱","#123","?1233d"};

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		requestWindowFeature(Window.FEATURE_NO_TITLE);
		setContentView(R.layout.activity_main);

		 lv_content = (ExpandableListView) findViewById(R.id.lv_content);
		
		final ArrayList<GoodMan> persons = new ArrayList<GoodMan>();;
		for(String str:NAMES)
		{
			GoodMan gm=new GoodMan(str);
			persons.add(gm);
		}
		/**加入支持泛型*/
		adapter=new PingyinAdapter<GoodMan>(lv_content,persons,R.layout.item_man){

			@Override
			public String getItemName(GoodMan goodMan) {
				return goodMan.getName();
			}
                /**返回viewholder持有*/
			@Override
			public ViewHolder getViewHolder(GoodMan goodMan) {
				/**View holder*/
				class DataViewHolder extends ViewHolder implements View.OnClickListener{
					public TextView tv_name;
					public DataViewHolder(GoodMan goodMan) {
						super(goodMan);
					}
					/**初始化*/
					@Override
					public ViewHolder getHolder(View view) {
						tv_name = (TextView) view.findViewById(R.id.tv_name);
						/**在这里设置点击事件*/
						view.setOnClickListener(this);
						return this;
					}
					/**显示数据*/
					@Override
					public void show() {
						tv_name.setText(getItem().getName());
					}
					/**点击事件*/
					@Override
					public void onClick(View v) {
						Toast.makeText(v.getContext(),getItem().getName(),Toast.LENGTH_SHORT).show();
					}
				}
				return new DataViewHolder(goodMan);
			}

			@Override
			public void onItemClick(GoodMan goodMan, View view, int position) {
				Toast.makeText(view.getContext(),position+" "+goodMan.getName(),Toast.LENGTH_SHORT).show();
			}
		};
		/**展开并设置adapter*/
		adapter.expandGroup();

		FancyIndexer mFancyIndexer = (FancyIndexer) findViewById(R.id.bar);
		mFancyIndexer.setOnTouchLetterChangedListener(new OnTouchLetterChangedListener() {
			
			@Override
			public void onTouchLetterChanged(String letter) {
				for(int i=0,j=adapter.getKeyMapList().getTypes().size();i<j;i++)
				{
					String str=adapter.getKeyMapList().getTypes().get(i);
					if(letter.toUpperCase().equals(str.toUpperCase())){
						/**跳转到选中的字母表*/
						lv_content.setSelectedGroup(i);
					}
				}
			}
		});
		
	}
}


License
=======

    Copyright 2015 PoplarTang

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
