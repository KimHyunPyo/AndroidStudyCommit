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
ListView에 View Holder 패턴을 강제로 적용하여 성능적인 이슈를 해결하고
각 아이템마다 애니메이션을 설정할수 있게 변화되어 좀더 다양한 custom 뷰를 구성할 수 있다.

http://gogorchg.tistory.com/entry/Android-RecyclerView-%EC%97%90%EC%84%9C-Scroll-%EC%A0%95%EB%B3%B4-%ED%98%95%ED%83%9C
스크롤정보

```

3. NFC tag

```
```
4. SharedPreference
```
```
5. Parcelable Object (pass the Custom Object by intent)
```
implements Parcelable 선언후
추상 메소드 구현 필요

 writeToParcel 과 protected Model(Parcel in)
구현시에 주의사항
메소드내에서 처리해주는 데이터중 null값이 존재한다면 그 다음값은 모두 null처리
따라서 우선순위에따라 데이터 처리 필요


```
6. AsyncTask

+ AsyncTack란 ?

```
안드로이드는 UI를 담당하는 메인 쓰레드가 존재하는데, 이 쓰레드는 우리가 함부로 접근이 불가능하게 막아뒀습니다.

그런데 UI변경은 메인 쓰레드에서만 가능하고, 우리가 만든 쓰레드에서는 화면을 바꾸는 어떠한 일도 할 수 없습니다.

이러한 이유로 안드로이드는 Background 작업을 할 수 있도록 AsyncTask를 지원합니다.

AsyncTask는 쓰레드와 핸들러를 통해 UI를 처리했던 것을 한번에 작업할 수 있도록 지원해줍니다.


즉, UI작업을 위해 만들어야 했던 Handler가 필요없어지는 겁니다.

개발할 때의 부담을 덜어줍니다.

또한 백그라운드 작업을 하면서 진행 상황을 사용자에게 보여줄 수 있는 CallBack 메소드도 지원하면서 말이죠.



 ※ AsyncTask = Thread + Handler


출처: http://itmir.tistory.com/624 [미르의 IT 정복기]
```


+ How To
```
public class MyAsyncTask extends AsyncTask<Integer, Integer, Integer> {

    @Override
    protected void onPreExecute() {
        super.onPreExecute();
        //백그라운드 작업 시작전 호출 준비작업 해주는곳
        //ex) 네트워크 준비 or 객체 생성
    }

    @Override
    protected Integer doInBackground(Integer... integers)
    //onPreExecute 이후 background에서 실행되는 작업
        return 0;
    }

    @Override
    protected void onProgressUpdate(Integer... params) {
      //doin이 실행되는 도중 publishProgress() 호출시에실행되는 Method

    }

    @Override
      protected void onPostExecute(Integer result) {
          super.onPostExecute(result);
          //doinBackgroud 작업 종료후 결과 값
      }
}

<>안의 제너릭에 들어가는 값은
void, Integer, String 등의 조합으로 사용가능
AsyncTask<doInBackground()의 변수 종류, onProgressUpdate()에서 사용할 변수 종류, onPostExecute()에서 사용할 변수종류>



doInBackground()의 변수 종류 : 우리가 정의한 AsyncTask를 execute할 때 전해줄 값의 종류
onProgressUpdate()에서 사용할 변수 종류 : 진행상황을 업데이트할 때 전달할 값의 종류
onPostExecute()에서 사용할 변수종류 : AsyncTask가 끝난 뒤 결과값의 종류


MyAsyncTask mProcessTask = new MyAsyncTask();
> onPreExecute()실행

mProcessTask.execute(value);
>value 값을 전달 받고 doInBackground()실행
>value값 참조위해서는 value

publishProgress(value)
>value 값을 전달 받고 onProgressUpdate() 실행



출처: http://itmir.tistory.com/624 [미르의 IT 정복기]


```

+  활용시 유의사항

```
**여러가지 값을 전달가능하고, 전달한 순서대로 전달받은 함수에서 배열의 인덱스로 참조가능.  다시 execute하면 에러가 발생한다.

```

7. GoogleVisionApi

8. GoogleTranslateApi
```
google cloud api 현재 안드로이드 지원 x
따라서 endpoint url인 https://www.googleapis.com/language/translate/v2?key= 에 쿼리문을 만들어서 요청을 해주고 json형식의 수신정보를 jsonparser를 이용해 파싱후 출력해야 한다.
이때 쿼리문의 형식은
https://www.googleapis.com/language/translate/v2?key=  + api_key &target=ko&source=ec&q="번역할 String utf-8인코딩"이다.

```


9. cURL

```
cURL(/kɝl/ 또는 /kə:l/[3])은 다양한 통신 프로토콜을 이용하여 데이터를 전송하기 위한 라이브러리와 명령 줄 도구를 제공하는 컴퓨터 소프트웨어 프로젝트이다. 이 cURL 프로젝트는 libcurl와 cURL이라는 2개의 제품을 만든다. 1997년에 처음 출시되었다. 이 이름은 "see URL"을 대표한다.
```


10. java URL과 httpsUrlconnetion을 이용한 요청 및 수신
```
1. url 객체의 요청하는 url 생성
 URL url = new URL(URL + GOOGLE_TRANSLATE_API +SOURCE+ TARGET + QEURY + encodedText);
 2.httpsUrlconnetion을 생성해 생성해둔 url로 커넥션 오픈
HttpsURLConnection conn = (HttpsURLConnection) url.openConnection();
(httpsUrlconnetion의 requsetcode가 200인 경우 정상 수신)
3.InputStream stream;
  BufferedReader reader = new BufferedReader(new InputStreamReader(stream));
를 이용해 버퍼를 이용해 인풋스트림에 내용을쓴다.
4.reader.line으로 내용을 가져온다.
```

11. PowerManager
```
//사용자가 다운로드 중 파워 버튼을 누르더라도 CPU가 잠들지 않도록 해서
//다시 파워버튼 누르면 그동안 다운로드가 진행되고 있게 됩니다.
PowerManager pm = (PowerManager) context.getSystemService(Context.POWER_SERVICE);
mWakeLock = pm.newWakeLock(PowerManager.PARTIAL_WAKE_LOCK, getClass().getName());
mWakeLock.acquire();
```

12. Annotation
소스 코드에 메타데이터를 표현하는 것입니다.
리플렉션을 이용하면 어노테이션 지정만드로도 원하는 클래스 주입하는것 가능
기본 제공 annotation
```
@Override - 메소드가 오버라이드 됐는지 검증합니다. 만약 부모 클래스 또는 구현해야할 인터페이스에서 해당 메소드를 찾을 수 없다면 컴파일 오류가 납니다.
@Deprecated - 메소드를 사용하지 말도록 유도합니다. 만약 사용한다면 컴파일 경고를 일으킵니다.
@SuppressWarnings - 컴파일 경고를 무시하도록 합니다.
@SafeVarargs - 제너릭 같은 가변인자 매개변수를 사용할 때 경고를 무시합니다. (자바7 이상)
@FunctionalInterface - 람다 함수등을 위한 인터페이스를 지정합니다. 메소드가 없거나 두개 이상 되면 컴파일 오류가 납니다. (자바 8이상)
```



13. spannable

문자열 데이터를 표한하기위한 클래스
 - spannable을 이용하면 textview 로 image도 출력가능
- 블로그 글처럼 동적으로 이미지와 텍스트를 같이 배치할때 사용 하면 좋다
- how to
```
1.  textview의 bufferType 을 spannable로 선언해준다.
2. img표현 방법
Drawable dr= ResourcesCompat.getDrawable(getResources(),R.drawable.imag,null);
dr.setBounds(0,0,dr.getIntrinsicWidth(),dr.getIntrinsicHeight());
ImageSpan span = new ImageSpan(dr);
spannableStringBuilder builder = new spannableStringBuilder(String);
builder.setSpan(span,start,end,Spenned.SPAN_EXCLUSIVE_EXCLUSIVE);

```


14. 중복실행 방지 텀을 가진 onClick만들고 모든 onClick에 적용하기



OnClick 이벤트를 처리하다보면 빠르게 여러번 클릭하는 경우 중복으로 클릭처리가 될 수 있다.

서버에 중복으로 요청이 될 수도있고 함수가 두번 실행 될수도 있다.

이런 부분을 방지하는 방법에는 여러가지가 있겠지만 개인적으로 View.OnClickListener를 구현하는 별도이 클래스를 만들어서 사용하는 방법을 선호한다.

먼저 View.OnClickListener를 구현하는 추상클래스를 만든다.


import android.os.SystemClock;
import android.view.View;

public abstract class OnSingleClickListener implements View.OnClickListener {
    // 중복 클릭 방지 시간 설정
    private static final long MIN_CLICK_INTERVAL=600;

    private long mLastClickTime;

    public abstract void onSingleClick(View v);

    @Override
    public final void onClick(View v) {
        long currentClickTime=SystemClock.uptimeMillis();
        long elapsedTime=currentClickTime-mLastClickTime;
        mLastClickTime=currentClickTime;

        // 중복 클릭인 경우
        if(elapsedTime<=MIN_CLICK_INTERVAL){
            return;
        }

        // 중복 클릭아 아니라면 추상함수 호출
        onSingleClick(v);        
    }

}
그리고 OnClickListener를 생성하는 코드 대신 OnSingleClickListener를 생성하는 코드를 사용하면 된다.

mTextView.setOnClickListener(new OnSingleClickListener() {
            @Override
            public void onSingleClick(View v) {
                // click 작업 수행
            }
     };
참고 URL


15. bitmap 이미지를 변환해서 파일로 저장하는 ImageSaver클래스

```

package com.example.pixelro.eyeclever.Utills;

import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.os.Environment;
import android.support.annotation.NonNull;
import android.util.Base64;
import android.util.Log;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class ImageSaver {

    private String directoryName = "images";
    private String fileName = "image.png";
    private Context context;
    private boolean external;

    public ImageSaver(Context context) {
        this.context = context;
    }

    public ImageSaver setFileName(String fileName) {
        this.fileName = fileName;
        return this;
    }

    public ImageSaver setExternal(boolean external) {
        this.external = external;
        return this;
    }

    public ImageSaver setDirectoryName(String directoryName) {
        this.directoryName = directoryName;
        return this;
    }


    public void delete(){
        createFile().delete();
    }

    public void save(Bitmap bitmapImage) {
        FileOutputStream fileOutputStream = null;
        try {
            fileOutputStream = new FileOutputStream(createFile());
            bitmapImage.compress(Bitmap.CompressFormat.PNG, 100, fileOutputStream);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                if (fileOutputStream != null) {
                    fileOutputStream.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    @NonNull
    public File createFile() {
        File directory;
        if(external){
            directory = getAlbumStorageDir(directoryName);
        }
        else {
            directory = context.getDir(directoryName, Context.MODE_PRIVATE);
        }
        if(!directory.exists() && !directory.mkdirs()){
            Log.e("ImageSaver","Error creating directory " + directory);
        }

        return new File(directory, fileName);
    }

    private File getAlbumStorageDir(String albumName) {
        return new File(Environment.getExternalStoragePublicDirectory(
                Environment.DIRECTORY_PICTURES), albumName);
    }

    public static boolean isExternalStorageWritable() {
        String state = Environment.getExternalStorageState();
        return Environment.MEDIA_MOUNTED.equals(state);
    }

    public static boolean isExternalStorageReadable() {
        String state = Environment.getExternalStorageState();
        return Environment.MEDIA_MOUNTED.equals(state) ||
                Environment.MEDIA_MOUNTED_READ_ONLY.equals(state);
    }

    public Bitmap load() {
        FileInputStream inputStream = null;
        try {
            inputStream = new FileInputStream(createFile());
            Log.d("ImageSaver","IamgeCapacity"+createFile().length()/1024+"KB");
            return BitmapFactory.decodeStream(inputStream);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try {
                if (inputStream != null) {
                    inputStream.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        return null;
    }
}

```

16. Bitmap 이미지와 String Resource간의 Base64 인코딩을 통한 변환 메소드를 가진
class
```
package com.example.pixelro.eyeclever.Utills;

import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.graphics.drawable.BitmapDrawable;
import android.support.v4.graphics.drawable.RoundedBitmapDrawable;
import android.util.Base64;
import android.widget.ImageView;

import java.io.ByteArrayOutputStream;

public class ImageUtill {
    public static Bitmap convertImageViewToBitmap(ImageView v) {
        Bitmap bm = null;
        try {
            bm = ((RoundedBitmapDrawable) v.getDrawable()).getBitmap();
        } catch (Exception e) {
            bm = ((BitmapDrawable) v.getDrawable()).getBitmap();
        }
        return bm;
    }
    public static Bitmap StringToBitMap(String encodedString){
        try{
            byte [] encodeByte=Base64.decode(encodedString, Base64.DEFAULT);
            Bitmap bitmap= BitmapFactory.decodeByteArray(encodeByte, 0, encodeByte.length);
            return bitmap;
        }catch(Exception e){
            e.getMessage();
        }
        return null;
    }
    public static String BitMapToString(Bitmap bitmap)
    {
        ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
        bitmap.compress(Bitmap.CompressFormat.PNG, 100, outputStream);
        return Base64.encodeToString(outputStream.toByteArray(), Base64.DEFAULT);
    }

}
```

- Android 사운드 관련

1. 현재 모드 가져오기
```
AudioManager am = (AudioManager) getSystemService(Context.AUDIO_SERVICE);
switch (am.getRingerMode()) {
    case AudioManager.RINGER_MODE_NORMAL:
        // 보통
    case AudioManager.RINGER_MODE_VIBRATE:
        // 진동
    case AudioManager.RINGER_MODE_SILENT:
        // 무음
}
```
2. 볼륨설정 가져오기

```
AudioManager am = (AudioManager) getSystemService(Context.AUDIO_SERVICE);
int 통화음량 = am.getStreamVolume(AudioManager.STREAM_VOICE_CALL);
int 시스템 = am.getStreamVolume(AudioManager.STREAM_SYSTEM);
int 벨소리 = am.getStreamVolume(AudioManager.STREAM_RING);
int 음악 = am.getStreamVolume(AudioManager.STREAM_MUSIC);
int 알람 = am.getStreamVolume(AudioManager.STREAM_ALARM);
int 통지 = am.getStreamVolume(AudioManager.STREAM_NOTIFICATION);

```


3. 게임에서 초기에 BGM설정하기

```

// VOLUME 조절이 가능하게 한다.
setVolumeControlStream(AudioManager.STREAM_MUSIC);

AudioManager am = (AudioManager) getSystemService(Context.AUDIO_SERVICE);
int currentVolumn = am.getStreamVolume(AudioManager.STREAM_SYSTEM);
Log.d("VPB", "currentVolumn="+currentVolumn);
switch (am.getRingerMode()) {
	case AudioManager.RINGER_MODE_SILENT:
		am.setStreamVolume(AudioManager.STREAM_MUSIC, 0, 0);
		break;
	case AudioManager.RINGER_MODE_VIBRATE:
		am.setStreamVolume(AudioManager.STREAM_MUSIC, 0, 0);
		break;
	case AudioManager.RINGER_MODE_NORMAL:
		am.setStreamVolume(AudioManager.STREAM_MUSIC, currentVolumn, 0);
		break;
}
bgmPlayer.start(); // BGMPlayer는 MediaPlayer를 구현한 클래스의 인스턴스.


```

노티 제거
```
NotificationManager notiManager = (NotificationManager) getApplicationContext().getSystemService(Context.NOTIFICATION_SERVICE);
                notiManager.cancel(LastNotiID);
  ```              
