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

2. ListView

3. NFC tag

4. SharedPreference
