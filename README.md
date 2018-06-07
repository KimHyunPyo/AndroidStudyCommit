# AndroidStudyCommit

# 2018.05.17부터 Pravacy Cover를 만들며 공부한 Android내용을 정리하는 공간.

1. Context

 + Context ?

```
어플리케이션 환경에 관한 글로벌 정보를 접근하기 위한 인터페이스.
안드로이드는 프로세스와 어플리케이션이 서로 다른개념으로 1:1 대응하지 않기 때문에 프로세스를 통해 어플리케이션을 구분할수 없다.
context를 통해 어플리케이션의 고유한 값을 부여하여 어플리케이션을 구분.

: 어플리케이션의 ID카드
```

 + 역할 및 용도

```
- 자신이 어떤 어플리케이션을 나타내고 있는지 알려주는 ID 역할
- ActivityManagerService 에 접근할 수 있도록 하는 통로 역할
- 어플리케이션과 관련된 정보에 접근하고자 하거나 어플리케이션과 연관된 시스템 레벨의 함수를 호출하고자 할 때 사용
```
+ Context의 특징

```
Application이 생성될 때 생성
Activity, Service, BroadcastRecieve같은 Application의 하위 컴포넌트들이 생성 될때 마다 생성.
 = 각각 컴포넌트들이 가지는 context가 다르다!
```

- 사용법

```
-Activity

this

-Adapter

adapter 생성시 this를 통해 Context를 넘긴다.

listadaptor = new RegisteredAppAdapter(RegistedAppViewActivity.this,
  R.layout.registered_package_list_layout,RegisterApplist);

생성자에서
this.context = context; 로 받아온다.
public RegisteredAppAdapter(Context context, int textViewResourceId,
                               List<ApplicationInfo> appsList) {
       super(context, textViewResourceId, appsList);
       this.context = context;
   }

packageManager = context.getPackageManager();
같은 사용법으로 호출한 activity의 구성요소에 접근가능.

-Application context에 접근

public Context getApplicationContext()
이용하여 언제든 부모 Context에 접근 가능

```

- 주요 METHOD

```


```

2. ListView & RecyclerView

 +  ListView?
 ```
Android App 제작시 UI구성에 필수적인 요소.
UI에서 보여줘야하는 ITEM의 갯수가 동적인 경우 각각의 뷰를 구성해주고 이 뷰를 리스트로 구현함으로써,
ITEM의 변화에따라 자동으로 변화된 ViEW를 제공해준다.
 ```


+ How To Use?
```
Adapter, Model을 이용해 구현한다.

Model : 각각의 VIEW가 가져야할 정보를 가지고있는 객체.

Adapter : BaseAdapter를 기본으로 상속받아 ArrayAdapter등이 있으며 model의 layout과 model의 LIST, acvtivity의 context를 생성자로 받아서 생성되어
생성자의 정보를 가지고 각각 모델의 view를 getView에서 만들어준다.
생성되는 UI의 순서는 model List의 index를 참조하여 낮은 숫자일수록 상단에 위치한다.

1.item의 model 객체 생성
2.각 item을 구성할 layout 생성
3.ArrayList<model> modelList 생성 및 item Add
4.ListView의 layout 구성
5.adapter의 getView에서 Model의 정보를 이용해 뷰에 텍스트 및 이미지 할당
5.ListView의 Acitivity에서 adapter를 생성 및 setAdapter.

```

 + RecyclerView
```


```

3. NFC tag

4. SharedPreference

5. Parcelable Object (pass the Custom Object by intent)

6.
