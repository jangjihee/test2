<!-- Heading -->
# Find the shoe store around - MM
## 목차
#### **1. 프로젝트 개요**<br>
#### **2. 프로젝트 일정**<br>
#### **3. 프로젝트 목표**<br>
#### **4. 개발 환경 및 데이스 베이스 설계**<br>
#### **5. 구현 동영상**<br>
#### **6. 개발 방법**<br>
#### **7. 프로젝트 소감**<br>


# **1. 프로젝트 개요**
## 1) 프로젝트 필요성
* 신발을 구매할때 자신의 근처에 있는 매장 정보를 확인할 수 있어 번거롭지 않음

* 직접 신발을 신어보고 구매를 원할 때 이 앱으로 편하게 매장을 찾아 신발을 구매할 수 있음

* 오프라인 매장에 방문해서 자신에게 맞는 신발 사이즈를 알 수 있음

* 이용자 주변에서 신발을 찾고싶을때 주변 매장을 확인 할 수 있음 

* 사람에 따라 원하는 사이즈와 종류를 이 앱으로 주변 매장을 알아보고 가까운 매장을 알 수 있음

## 2) 프로젝트 차별성 
![슈픽](https://user-images.githubusercontent.com/48505742/59295030-ad8e4300-8cbd-11e9-8415-da8679d9988e.png)

* 내 주변 매장을 검색해 신발을 찾을 수 있음

* 오프라인 매장에 직접 방문 해서 직접 신어보고 비교할 수 있음

* 매장에서 자신의 신발 사이즈가 있는지 확인 할 수 있음

* 다양한 신발매장 확인가능함

* 화면으로 볼때보다 더 자세하게 신발을 확인가능

* 메모기능과 실시간 채팅방 기능으로 앱 이용자들 간에 정보를 공유 할 수 있음.


# **2. 프로젝트 일정**
* 2019.03.06 ~ 2019.06.19<br>
                            ![개발 일정](https://user-images.githubusercontent.com/48505742/59264897-173b2c80-8c7f-11e9-963d-a6d3fbdabbb1.PNG)

# **3. 프로젝트 목표**

* 주변 신발 매장을 찾지 못하고 헤매고 번거로움에 온라인 쇼핑을 하는 사람들을 위해 만들었음

* 위치기반 서비스를 이용한 주변 신발 매장을 알 수 있고, 사용자가 신발을 사고자 할 때 주변에 원하는 매장, 신발이 있는지 알 수 있음

* 사용자의 오프라인 매장 방문 찾기를 도와 신발 매장의 위치를 확인할 수 있음

* 사용자의 취향에 맞게 다양한 매장을 찾아줌

# **4. 개발 환경 및 데이터 베이스 설계**
* 개발 환경<br>
                            ![개발 환경](https://user-images.githubusercontent.com/48505742/59225106-d99cbc00-8c0a-11e9-9ef2-eeed0b0cfb72.PNG)<br>
* 데이터 베이스 설계<br>
                            ![디비](https://user-images.githubusercontent.com/48505742/59224981-99d5d480-8c0a-11e9-98f2-08e8831bfd92.jpg)
<br>

# **5. 구현 동영상**
<!-- Links -->
[YouTube](https://youtu.be/vgZgf0mSrzI "유튜브")

# **6. 개발 방법**

### 1. JSON을 활용한 ANDROID와 WEB SERVER & ORACLE 연동 로그인
* Android 생성 버전 설정.
> Application name : M_M<br>
  Android Devices - Minimun SDK API 15 : Android 4.0.3<br>
  Add an activity to Mobile : Empty Activity<br/>

> "json_simple-1.1.jar" , "ojdbc6.jar" 파일 구글에 검색해서 다운.<br>

* Android Studio에 JAR 파일 추가 방법. <br>
![jar 1](https://user-images.githubusercontent.com/48506075/59367628-78462b80-8d77-11e9-9d20-a3b0f9105c14.PNG)<br>
![jar 2](https://user-images.githubusercontent.com/48506075/59367688-96139080-8d77-11e9-9981-e3113c09f141.PNG)<br>
![jar 3](https://user-images.githubusercontent.com/48506075/59367689-96ac2700-8d77-11e9-9c7d-2108bc9d5074.PNG)<br>



* 로그인 화면(activity_main.xml) 제작. <br>
![3](https://user-images.githubusercontent.com/48506075/59369600-bba29900-8d7b-11e9-9dcf-5513ca89c6a3.PNG)<br>

* MainActivity.java 에 버튼 이벤트 설정

```
  //회원가입 화면으로 버튼 
  Button btn02 = (Button) findViewById(R.id.registerButton); 
        btn02.setOnClickListener(new View.OnClickListener(){
            @Override
            public void onClick(View v){
                Intent intent = new Intent(getApplicationContext(), RegisterActivity.class);
                startActivity(intent);
            }
        }); 
```

* 회원가입 화면 (activity_register.xml) 제작.<br>
![4](https://user-images.githubusercontent.com/48506075/59369702-ef7dbe80-8d7b-11e9-9cbf-8279b113f2b0.PNG)<br>


* RegisterActivity.java 제작

```
// 네트워크 쓰레드 관리 메소드
StrictMode.setThreadPolicy(new StrictMode.ThreadPolicy.Builder()
                .detectDiskReads().detectDiskWrites().detectNetwork().penaltyLog().build());
        if (Build.VERSION.SDK_INT > 9) {
            StrictMode.ThreadPolicy policy = new StrictMode.ThreadPolicy.Builder().permitAll().build();
            StrictMode.setThreadPolicy(policy);
        }
```
```
/// 정보 입력후 회원가입 버튼 클릭 시 이벤트
        btnSend.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                // 보내는 메시지를 받아옴
                String sMessage1 = etMessage1.getText().toString();
                String sMessage2 = etMessage2.getText().toString();
                String sMessage3 = etMessage3.getText().toString();
                String sMessage4 = etMessage4.getText().toString();

                // 한번에 보낼 sMessage 생성
                String sMessage;
                // 보내는 형식 지정
                sMessage = sMessage1 + "/" + sMessage2 + "/" + sMessage3 + "/" + sMessage4;
                // 메시지를 서버에 보냄
                String result = SendByHttp(sMessage);
                // 연동 후 받아온 데이터 파싱
                String[][] parsedData = jsonParserList(result);

            }
        });
    }
```

```
/// 서버에 데이터를 보내는 메소드 
    private String SendByHttp(String msg) {
        if(msg == null )
            msg = "";

        String URL = "http://자신의 컴퓨터 IP:8080/" + "이 후 만들 WEBSERVER 파일명";

        DefaultHttpClient client = new DefaultHttpClient();

        try {

            HttpPost post = new HttpPost(URL + "?msg=" + msg);

            /* 지연시간 최대 5초 */
            HttpParams params = client.getParams();
            HttpConnectionParams.setConnectionTimeout(params, 3000);
            HttpConnectionParams.setSoTimeout(params, 3000);

            /* 데이터 보낸 뒤 서버에서 데이터를 받아오는 과정 */
            HttpResponse response = client.execute(post);
            BufferedReader bufreader = new BufferedReader(
                    new InputStreamReader(response.getEntity().getContent(),"utf-8"));

            String line = null;
            String result = "";

            while ((line = bufreader.readLine()) != null) {
                result += line;
            }

            return result;
        } catch (Exception e) {
            e.printStackTrace();
            client.getConnectionManager().shutdown(); // 연결 지연 종료
            return "";
        }
    }

```

* build.gradle (Module: app)에 아파치 HTTP을 dependencies 추가하기 <br>
> compileOnly 'org.jbundle.util.osgi.wrapped:org.jbundle.util.osgi.wrapped.org.apache.http.client:4.1.2'<br>

* andriodManifest.xml 에 INTERNET 허가<br> 
> <user-permission android:name="android:name="andriod.permission.INTERNET"/> <br>

* Eclipse에 JAVA WEBSERVER(mm) <br>
 Dynamic Web Project 생성 후 WebContent에 Join.jsp 생성.<br>
![java1](https://user-images.githubusercontent.com/48506075/59368171-9fe9c380-8d78-11e9-87fe-67fd4c520c34.png) <br>
* Join.jsp 작성(Eclipse)
```
    <%
	String recvMessage = "0";
	String[] msg;
	String Message1 = "1";
	String Message2 = "2";
	String Message3 = "3";
	String Message4 = "4";
	String Message5 = "5";
	String Message6 = "6";
	String Message7 = "7";
	String Message8 = "8";
	

	    try {
            recvMessage = request.getParameter("msg");
            // 받아 온 msg 를 "/"를 기준으로 배열에 0번 부터 차례대로 Mseeage1 에 지정.
            if (recvMessage != null) {
                msg = recvMessage.split("/");
                Message1 = msg[0];
                Message2 = msg[1];
                Message3 = msg[2];
                Message4 = msg[3];
            }
            
            //////////////// DB 연결 ////////////////
            Connection conn = null;
            Statement stmt = null;
            ResultSet rs = null;
            String sql = null;
            ResultSet rss = null;
            String sqls = null;
            Statement stmts = null;
            
            try {
                Class.forName("oracle.jdbc.driver.OracleDriver");
                conn = DriverManager.getConnection(
                        "jdbc:oracle:thin:@자신 서버 IP:1521:orcl", "NAME", "PASSWORD");
                
                try{
                    // 테이블에 INSTERT 하는 부분.
                    sql = "INSERT INTO MM__MEMBER VALUES('" + Message1 + "', '";
                    sql = sql + Message2 + ","+ Message3 + "," + Message4 +"')";
                    stmt = conn.createStatement();
                    rs = stmt.executeQuery(sql);
                    rs.close();
                    stmt.close();
                    
                } catch(Exception e) {
                    System.out.println("오라클 Insert 오류!");
                }

            } catch(Exception e) {
                System.out.println("오라클 연동 실패!");
            }
        } catch(Exception e) {
            System.out.println("서버 및 오라클 오류!");
        } finally {
            JSONObject jsonMain = new JSONObject();
            JSONArray jArray = new JSONArray();
            JSONObject jObject = new JSONObject();
            //받아 온 값 리턴 값 으로 담는 부분.
            jObject.put("msg1", Message5);
            jObject.put("msg2", Message6);
            jObject.put("msg3", Message7);
            jObject.put("msg4", Message8);
        
            
            jArray.add(0, jObject);
            jsonMain.put("List", jArray);
            out.println(jsonMain.toJSONString());
        }
    %>
```

* 로그인하는 MainActivty.java 제작 <br>

```
   
        /* Send 버튼을 눌렀을 때 서버에 데이터를 보내고 받는다 */
        btnSend.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                // 보내는 메시지를 받아옴
                String sId = edId.getText().toString();
                String sPass = edPass.getText().toString();

                String msg = sId + "/" + sPass;

                // 메시지를 서버에 보냄
                String result = SendByHttp(msg);

                // JSON 데이터 파싱
                String parsedData = jsonParserList(result);

                Toast.makeText(getApplicationContext(), parsedData, Toast.LENGTH_SHORT).show();

                if (parsedData.equals("로그인성공")) {
                    Intent loginIntent = new Intent(getApplicationContext(),OkActivity.class);
                    MainActivity.this.startActivity(loginIntent);
                } else {
                    Toast.makeText(getApplicationContext(), "아이디와 비번을 확인해주세요.",
                            Toast.LENGTH_SHORT).show();
                }
            }
        });
    }
```

* WebContent에 ServerDB.jsp 작성(Eclipse)<br>
```
<%
	String getMsg = "0";
	String[] arr;
	String getid = "0"; // 안드로이드에서 불러오는 아이디
	String getpass = "0"; // 안드로이드에서 불러오는 패스워드
	int x = 0;
	
	// 서버에서 받아온 아이디/비밀번호 를 /단위로 나누어 각각 객체에 넣음
	getMsg = request.getParameter("msg");
	if(getMsg != null) {
		arr = getMsg.split("/");
		getid = arr[0];
		getpass = arr[1];
	}

	//////////////// DB 연결 ////////////////
	Connection conn = null;
	Statement stmt = null;
	ResultSet rs = null;
	String sql = null;

	try {
		Class.forName("oracle.jdbc.driver.OracleDriver");
		conn = DriverManager.getConnection("jdbc:oracle:thin:@서버 IP:orcl", "NAME", "PASS");
		x = 0;
		try {
			sql = "SELECT MM_ID, MM_PWD FROM MM_MEMBER WHERE MM_ID = '" + getid + "' AND MM_PWD = '" + getpass + "'";
			stmt = conn.createStatement();
			rs = stmt.executeQuery(sql);
			// 적은 아이디 비번을 디비와 비교하고 결과 값 보내 주는 부분.
			while (rs.next()) {
				if (getid.equals(rs.getString("id")))
				{
					if (getpass.equals(rs.getString("pass")))
					{
						x = 1; // 로그인 성공
					} else x = 0; // 로그인 실패
				} else x = 0; // 로그인 실패
			}
			
			rs.close();
			stmt.close();
		} catch (Exception e) {
			System.out.println("SQL문 오류");
		}
		
	} catch (Exception e) {
		System.out.println("오라클 연동 실패!");
	} finally {
		JSONObject jObject = new JSONObject();
		
		if(x==1){
			jObject.put("msg", "로그인성공");
		} else {
			jObject.put("msg", "로그인실패");
		}

		out.println(jObject.toJSONString());
	}
%>
```
---
### 2. Firebase 기반 실시간 채팅 .
https://mailmail.tistory.com/44 <br>
본 사이트를 보고 프로젝트에 Firebase를 연동 시켜준다.

* 데이터베이스 사용에 관한 dependency를 추가 해준다. 
```
//build.gradle(Moudule: app)
//dependencies 안에 추가
implementation 'com.google.firebase:firebase-database:17.0.0'
```
* 채팅방 입장 화면 생성(.XML)<br>
![9](https://user-images.githubusercontent.com/48506075/59371896-2bffe900-8d81-11e9-8fff-2583d5bbf874.PNG)<br>


* StartActivity.java 파일 생성.
```
/// 데이터베이스의 인스턴스를 불러온다.
    private FirebaseDatabase firebaseDatabase = FirebaseDatabase.getInstance();
    private DatabaseReference databaseReference = firebaseDatabase.getReference();
```

```
// 채팅방 이름과 유저 이름 입력 후 GO 버튼 클릭시 이벤트
 user_next.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (user_edit.getText().toString().equals("") || user_chat.getText().toString().equals(""))
                    return;

                Intent intent = new Intent(StartActivity.this, ChatActivity.class);
                intent.putExtra("chatName", user_chat.getText().toString());
                intent.putExtra("userName", user_edit.getText().toString());
                startActivity(intent);
            }
        });

        showChatList();

    }
```
```
// 화면 밑에 채팅방 리스트 
private void showChatList() {
        // 리스트 어댑터 생성 및 세팅
        final ArrayAdapter<String> adapter

                = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, android.R.id.text1);
        chat_list.setAdapter(adapter);

        // 데이터 받아오기 및 어댑터 데이터 추가 및 삭제 등..리스너 관리
        databaseReference.child("chat").addChildEventListener(new ChildEventListener() {
            @Override
            public void onChildAdded(DataSnapshot dataSnapshot, String s) {
                Log.e("LOG", "dataSnapshot.getKey() : " + dataSnapshot.getKey());
                adapter.add(dataSnapshot.getKey());
            }

```

* StartActivity.java 추가<br>
```
// 위젯 ID 참조
        chat_view = (ListView) findViewById(R.id.chat_view);
        chat_edit = (EditText) findViewById(R.id.chat_edit);
        chat_send = (Button) findViewById(R.id.chat_sent);

        // 로그인 화면에서 받아온 채팅방 이름, 유저 이름 저장
        Intent intent = getIntent();
        CHAT_NAME = intent.getStringExtra("chatName");
        USER_NAME = intent.getStringExtra("userName");

        // 채팅 방 입장
        openChat(CHAT_NAME);
        
        // 메시지 전송 버튼에 대한 클릭 리스너 지정
        chat_send.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (chat_edit.getText().toString().equals(""))
                    return;

                ChatDTO chat = new ChatDTO(USER_NAME, chat_edit.getText().toString()); //ChatDTO를 이용하여 데이터를 묶는다.
                databaseReference.child("chat").child(CHAT_NAME).push().setValue(chat); // 데이터 푸쉬
                chat_edit.setText(""); //입력창 초기화

            }
        });
    }
```

* 채팅 화면 생성(.XML)<br>
![10](https://user-images.githubusercontent.com/48506075/59371898-2e624300-8d81-11e9-8a3e-a725146f3b43.PNG)<br>

* ChatActivity.java 파일 생성.<br>
```
 // StartActivity에서 받아온 채팅방 이름과 사용자 아이디 받아오는 부분.
 // 위젯 ID 참조
        chat_view = (ListView) findViewById(R.id.chat_view);
        chat_edit = (EditText) findViewById(R.id.chat_edit);
        chat_send = (Button) findViewById(R.id.chat_sent);

        // 로그인 화면에서 받아온 채팅방 이름, 유저 이름 저장
        Intent intent = getIntent();
        CHAT_NAME = intent.getStringExtra("chatName");
        USER_NAME = intent.getStringExtra("userName");

        // 채팅 방 입장
        openChat(CHAT_NAME);

        // 메시지 전송 버튼에 대한 클릭 리스너 지정
        chat_send.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (chat_edit.getText().toString().equals(""))
                    return;
                // 채팅 입력이 데이터 전송되는 부분 설정.
                ChatDTO chat = new ChatDTO(USER_NAME, chat_edit.getText().toString()); //ChatDTO를 이용하여 데이터를 묶는다.
                databaseReference.child("chat").child(CHAT_NAME).push().setValue(chat); // 데이터 푸쉬
                chat_edit.setText(""); //입력창 초기화

            }
        });
    }

```

* ChatDTO.JAVA 생성
```
// 속성에 접근하기 위한 getter,setter 메소드만 가진 클래스.
//DTO(Data Transfer Object) 
public class ChatDTO {

    private String userName;
    private String message;

    public ChatDTO() {}
    public ChatDTO(String userName, String message) {
        this.userName = userName;
        this.message = message;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public void setMessage(String message) {
        this.message = message;
    }

    public String getUserName() {
        return userName;
    }

    public String getMessage() {
        return message;
    }
}

```
* 결과 화면 <br>
![실시](https://user-images.githubusercontent.com/48506075/59379566-e992d800-8d91-11e9-8c80-1af3842ed7b2.PNG)


---
### 3. DrawerActivity로 사이드 메뉴 생성 <br>
![11](https://user-images.githubusercontent.com/48506075/59373242-3b346600-8d84-11e9-9888-e4545824bef2.PNG)<br>

* activity_main.xml에 수정
```
// DrawerLayout으로 수정해준다.
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

```

```
//DrawerLayout안의 layout_gravity="start" 추가
 <LinearLayout
        android:orientation="vertical"
        android:layout_width="280dp"
        android:layout_height="match_parent"
        android:weightSum="100"
        android:layout_gravity="start"
        android:background="#B0E0E6">

```
* 스마트 폰 설정하는 기능.
```
// 설정 버튼 클릭 시 이벤트 설정.
 set.setOnClickListener(new View.OnClickListener(){

            @Override
            public void onClick(View v){
                Intent intent = new Intent(Settings.ACTION_SETTINGS);

                startActivityForResult(intent, 0);
            }
        });


```

* 스마트 폰 진동, 소리 변경하는 기능.
```
//AndroidManifest.xml
<uses-permission android:name="android.permission.VIBRATE"/>
```

```
//MainActivity.java 추가
AudioManager am;

   // Switch 버튼 선언.
   Switch sw = (Switch)findViewById(R.id.jd);
   // 버튼 값에 다른 AudioManager 설정 변경
   sw.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
                if (isChecked == true){
                    am.setRingerMode(AudioManager.RINGER_MODE_VIBRATE);
                } else {
                    am.setRingerMode(AudioManager.RINGER_MODE_NORMAL);
                }
            }
        });
```
* 스마트 폰 절전모드 기능.
```
//MainActivity.java 추가
    PowerManager.WakeLock wakeLock;
    PowerManager powerManager;
```
```
//sw2 버튼 선언
Switch sw2 = (Switch)findViewById(R.id.jjj);
//wakeLock 선언
wakeLock = null;
powerManager = (PowerManager)getSystemService(POWER_SERVICE);
//sw2 버튼 클릭시 체크 값에 따른 이벤트 선언.
sw2.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @SuppressLint("InvalidWakeLockTag")
            @Override
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
                if (isChecked == true){
                    Intent batterySaverIntent=new Intent(Settings.ACTION_BATTERY_SAVER_SETTINGS);
                    startActivity(batterySaverIntent);
                } else {
                    wakeLock = powerManager.newWakeLock(PowerManager.FULL_WAKE_LOCK, "wakelock");
                    wakeLock.acquire();
                }
            }
        });
```
---
### 4. 상단바 및 달력 메뉴 생성 <br>
![15](https://user-images.githubusercontent.com/48506075/59377308-e517f080-8d8c-11e9-8745-3ac276ba7ae6.PNG)<br>

* activity_login.xml 수정.
```
// 상단바를 사용하기 때문에 LinearLayout ID값 지정.
  <LinearLayout
                android:id="@+id/linearLayout4"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:orientation="vertical"
                >
                <DatePicker
                    android:id="@+id/datePic01"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:layout_weight="2"
                    android:calendarViewShown="true"/>

                <EditText
                    android:id="@+id/edtDiary"
                    android:layout_width="match_parent"
                    android:layout_height="100dp"
                    android:background="#ff4182"
                    android:hint="이곳에 메모를 적으세요!"
                    android:lines="5"/>

                <Button
                    android:id="@+id/btn445"
                    android:layout_width="match_parent"
                    android:layout_height="50dp"
                    android:enabled="false"
                    android:text="확인"/>

            </LinearLayout>
```

* LoginActivity.java 생성
```
// tabHost에  메뉴 설정후 Layout id 값으로 불러오는 부분.
tabHost = (TabHost) findViewById(R.id.tabHost);
        tabHost.setup();

        TabHost.TabSpec spec1 = tabHost.newTabSpec("Tab1")
                .setContent(R.id.linearLayout3).setIndicator("소개");
        tabHost.addTab(spec1);

        TabHost.TabSpec spec2 = tabHost.newTabSpec("Tab2")
                .setContent(R.id.linearLayout2).setIndicator("게시판");
        tabHost.addTab(spec2);

        TabHost.TabSpec spec3 = tabHost.newTabSpec("Tab3")
                .setContent(R.id.linearLayout1).setIndicator("지도");
        tabHost.addTab(spec3);

        TabHost.TabSpec spec4 = tabHost.newTabSpec("Tab4")
                .setContent(R.id.linearLayout4).setIndicator("달력");
        tabHost.addTab(spec4);

        tabHost.setOnTabChangedListener(new TabHost.OnTabChangeListener() {
            @Override
            public void onTabChanged(String tabld) {
                if (tabld.equals("Tab1")) {

                } else if (tabld.equals("Tab2")) {

                } else if (tabld.equals("Tab3")) {

                } else if (tabld.equals("Tab4")) {

                }
            }
        });
```
* 달력 생성 (LoginActivity.java 추가)
```
// 달력 생성과 메모 입력 부분 버튼 선언.
dp = (DatePicker) findViewById(R.id.datePic01);
edtDiary = (EditText) findViewById(R.id.edtDiary);
btnWrite = (Button) findViewById(R.id.btn445);
// 달력 생성 부분.
Calendar cal = Calendar.getInstance();
int cYear = cal.get(Calendar.YEAR);
int cMonth = cal.get(Calendar.MONTH);
int cDay = cal.get(Calendar.DAY_OF_MONTH);
```

* 기존 달력에 추가한 메모 불러오는 부분 (LoginActivity.java 추가)
```
dp.init(cYear, cMonth, cDay, new DatePicker.OnDateChangedListener() {
            @Override
            public void onDateChanged(DatePicker view, int year, int monthOfYear, int dayOfMonth) {
                fileName = Integer.toString(year) + "-"
                        + Integer.toString(monthOfYear) + "-"
                        + Integer.toString(dayOfMonth) + ".txt";
                String str = readDiary(fileName);
                edtDiary.setText(str);
                btnWrite.setEnabled(true);
            }

        });
```

* 달력에 메모 추가하는 부분 (LoginActivity.java 추가)
```
btnWrite.setOnClickListener(new View.OnClickListener() {
                        @Override
                        public void onClick(View v) {
                            try {
                                FileOutputStream outFs = openFileOutput(fileName,
                                        Context.MODE_PRIVATE);
                                String str = edtDiary.getText().toString();
                                outFs.write(str.getBytes());
                                outFs.close();
                                Toast.makeText(getApplicationContext(), fileName + "이 저장됨",
                                        Toast.LENGTH_SHORT).show();
                            } catch (FileNotFoundException e) {
                                e.printStackTrace();
                            } catch (IOException e) {
                                e.printStackTrace();
                }
            }
        });
```
---
### 5. Main 화면 이미지 애니메이션 


* 구현 화면<br>
![애니13](https://user-images.githubusercontent.com/48506075/59401057-72326800-8dd4-11e9-9f59-433831d17fea.PNG)
![애니14](https://user-images.githubusercontent.com/48506075/59401056-72326800-8dd4-11e9-87eb-2f0ae6c197a3.PNG)

* login.xml에 코드 추가<br>
```
// activity_login.xml 에 탭 위치에 맞게  작성.
 <FrameLayout
                    android:id="@+id/linearLayout3"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:orientation="vertical"
                    >
                    <ImageView
                        android:layout_width="wrap_content"
                        android:layout_height="wrap_content"
                        android:id="@+id/skyImage"/>
                    <RelativeLayout
                        android:layout_width="match_parent"
                        android:layout_height="wrap_content">
                        <ImageView
                            android:layout_width="wrap_content"
                            android:layout_height="wrap_content"
                            android:id="@+id/swingImage"
                            android:layout_centerHorizontal="true"
                           android:background="@drawable/android_swing"/>

                    </RelativeLayout>
                </FrameLayout>
```
* res 폴더에 anim 폴더 생성 해주기.<br>
![an1](https://user-images.githubusercontent.com/48506075/59400118-4eb9ee00-8dd1-11e9-8da5-3a269875f46b.png)<br>
![애니2](https://user-images.githubusercontent.com/48506075/59400173-7f018c80-8dd1-11e9-9b23-7104b590924a.PNG)<br>
* anim폴더 안에 flow.xml 과 shake.xml 파일 생성<br>
![애니3](https://user-images.githubusercontent.com/48506075/59400214-a9ebe080-8dd1-11e9-8316-f9088902dbe3.png)<br>
![애니4](https://user-images.githubusercontent.com/48506075/59400221-ace6d100-8dd1-11e9-8935-21459ff5d65f.PNG)<br>
![애니5](https://user-images.githubusercontent.com/48506075/59400222-ace6d100-8dd1-11e9-83bf-246ab8a7fa40.PNG)<br>

* flow.xml 작성
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
<translate
    android:fromXDelta="0%p"
    android:toXDelta="-100%p"
    android:duration="20000"
    android:repeatCount="-1"/>
    <alpha
        android:toAlpha="0.5"
        android:fromAlpha="0.5"
        android:duration="20000"
        android:repeatCount="-1"/>
</set>

```
* skake.xml 작성
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">
    <rotate
        android:duration="1000"
        android:repeatCount="-1"
        android:repeatMode="reverse"
        android:pivotX="50%"
        android:pivotY="0%"
        android:fromDegrees="-30"
        android:toDegrees="30"
        android:toYScale="0.0"
        />
</set>
```
* Java 코드 추가(LoginActivity.java)
```
// 선언
 ImageView skyImage;
 ImageView swingImage;
    
 Animation flowAnimation;
 Animation shakeAnimation;


    swingImage = (ImageView)findViewById(R.id.swingImage);
    shakeAnimation = AnimationUtils.loadAnimation(this,R.anim.shake);
    swingImage.setAnimation(shakeAnimation);

    skyImage = (ImageView)findViewById(R.id.skyImage);
    flowAnimation = AnimationUtils.loadAnimation(this,R.anim.flow);
    skyImage.setAnimation(flowAnimation);

    Resources res = getResources();
    Bitmap bitmap = BitmapFactory.decodeResource(res, R.drawable.sky_background);

    int bitmapWidth = bitmap.getWidth();
    int bitmapHeight = bitmap.getHeight();

    ViewGroup.LayoutParams params = skyImage.getLayoutParams();
    params.width = bitmapWidth;
    params.height =bitmapHeight;

    skyImage.setImageBitmap(bitmap);
    flowAnimation.setAnimationListener(new AnimationAdapter());

```
* 메소드 추가<br>
![애니11](https://user-images.githubusercontent.com/48506075/59400352-1cf55700-8dd2-11e9-85a3-ad5618877d49.PNG)<br>
* 총 3개의 메소드 추가 <br>
![애니12](https://user-images.githubusercontent.com/48506075/59400353-1cf55700-8dd2-11e9-8b55-a6d97b35d2c8.PNG)<br>

* 추가생성한 메소드 중 한 onWindowFocusChanged 에 추가
```
 @Override
    public void onWindowFocusChanged(boolean hasFocus) {
        super.onWindowFocusChanged(hasFocus);
        if(hasFocus){
            shakeAnimation.start();

            flowAnimation.start();
        }else {
            shakeAnimation.reset();

            flowAnimation.reset();

        }
    }
```
* 추가 작성.
```
 private  final  class AnimationAdapter implements Animation.AnimationListener{


        @Override
        public void onAnimationStart(Animation animation) {

        }

        @Override
        public void onAnimationEnd(Animation animation) {

        }

        @Override
        public void onAnimationRepeat(Animation animation) {

        }
    }
```
---
### 6.Google Map

* Google Maps Android API와 Places API Web Service를 설정하기.

  먼저 Google Maps Android API를 설정하겠습니다. 구글 계정을 만들고 Google API Console (https://console.developers.google.com/apis/dashboard )에 접속하여 만들기를 클릭합니다.<br>
  ![ggapi1_1](https://user-images.githubusercontent.com/48506075/59369550-a463ab80-8d7b-11e9-826c-60d2a23c51aa.png)<br>

  프로젝트 이름을 적고 만들기를 클릭합니다.<br>
  ![ggapi1_2](https://user-images.githubusercontent.com/48506075/59369613-be04f300-8d7b-11e9-9666-a1b268e3a942.PNG)<br>

  새로운 프로젝트 생성을 완료합니다. API 및 사용 서비스 사용 설정을 클릭합니다.<br>
  ![ggapi1_3](https://user-images.githubusercontent.com/48506075/59371746-d297ba00-8d80-11e9-869a-7ba39fcce8b8.png)

  
  Maps SDK for Android를 선택하고 사용 설정을 클릭합니다.<br>
  ![ggapi1_4](https://user-images.githubusercontent.com/48506075/59368212-b5f78400-8d78-11e9-82f9-334d8c98d123.PNG)
  ![ggapi1_5](https://user-images.githubusercontent.com/48506075/59369668-decd4880-8d7b-11e9-86cb-6176d2086e2b.png)<br>

  사용자 인증 정보를 클릭합니다. 사용자 인증 정보 만들기를 클릭하여 보이는 메뉴에서 API 키를 클릭합니다.<br>
  ![ggapi1_6](https://user-images.githubusercontent.com/48506075/59369747-08866f80-8d7c-11e9-8570-c2febf6b25d3.png)<br>

  API가 활성화 되었습니다. 키 제한을 클릭합니다.<br>
  ![ggapi1_7](https://user-images.githubusercontent.com/48506075/59369810-2ce24c00-8d7c-11e9-9c44-b73f9fdb72ba.png)<br>

  API 키에 사용 제한을 둡니다. 어플리케이션 제한사항, API 제한사항을 설정합니다.<br>
  ![ggapi1_8](https://user-images.githubusercontent.com/48506075/59368457-3c13ca80-8d79-11e9-9884-9fb6164120ce.PNG)<br>

  Android 앱을 선택하고 항목 추가에 사용할 Android Project의 패키지 이름과 컴퓨터에서 생성된 SHA-1 인증서 지문을 입력합니다.<br>
  ![ggapi1_9](https://user-images.githubusercontent.com/48506075/59368483-4afa7d00-8d79-11e9-80b2-17b7608ebb36.PNG)<br>

  SHA-1 인증서 지문을 얻기 위한 과정입니다. 원도우키 + R을 누른 후 cmd를 입력하여 명령 프롬프트 창을 엽니다. 웹페이지에 제공된 윈도우용 명령을 복사하여 붙여으면 SHA-1 인증서 지문을 얻을 수 있습니다.<br>
  ![ggapi1_13](https://user-images.githubusercontent.com/48506075/59368514-5baaf300-8d79-11e9-94a7-09686db6e376.PNG)
  ![ggapi1_11](https://user-images.githubusercontent.com/48506075/59368532-68c7e200-8d79-11e9-8805-c0151e7c7840.PNG)<br>

  API 제한사항에서  키 제한을 선택하고 콤보박스에서 Maps SDK for Android를 체크합니다.  이제 저장을 클릭합니다.<br>
  ![ggapi1_10](https://user-images.githubusercontent.com/48506075/59368590-92810900-8d79-11e9-9d2d-f9f59a461bb7.PNG)<br>

  API 키를 복사해둡니다.<br>
  ![ggapi1_12](https://user-images.githubusercontent.com/48506075/59370056-b1cd6580-8d7c-11e9-9a86-0ad941eaee0b.png)<br>

  Google Maps Android API를 사용하려면 Google Play Services 라이브러리 패키지를 설치해줘야 합니다. Tools > SDK Manager > SDK Tools > Google Play Services 항목을 체크하고 Apply를 클릭하여 설치를 진행합니다.<br>
  ![ggapi1_14](https://user-images.githubusercontent.com/48506075/59368657-b0e70480-8d79-11e9-9e80-9f32a4b6cacd.png)<br>
 

  Places API Web Service는 Google Developers Console 사이트(https://console.developers.google.com/flows/enableapi?apiid=places_backend&reusekey=true&hl=ko )에 접속합니다. <br>
  콤보박스를 클릭하여 Google Maps Android API를 위해 생성했던 프로젝트를 선택하고 계속을 클릭합니다.<br> 
  ![ggapi2_1](https://user-images.githubusercontent.com/48506075/59368786-f1468280-8d79-11e9-96de-a24a3908ad21.PNG)<br>

  어떤 사용자 인증 정보가 필요한가요?를 클릭합니다.<br>
  ![ggapi2_2](https://user-images.githubusercontent.com/48506075/59368809-fa375400-8d79-11e9-986e-56c925c87bf5.PNG)<br>

  생성된  API키를 복사해두고 완료를 클릭합니다. <br>
  ![ggapi2_3](https://user-images.githubusercontent.com/48506075/59370253-18528380-8d7d-11e9-868b-e899a5a10f2a.png)<br>


* Project 생성<br>
![st0](https://user-images.githubusercontent.com/48506075/59379612-0af3c400-8d92-11e9-86af-3702df8d77b4.png)<br>
![st1](https://user-images.githubusercontent.com/48506075/59379045-a7b56200-8d90-11e9-82bd-cc9a486bb2db.PNG)<br>
![st2](https://user-images.githubusercontent.com/48506075/59381384-3082cc80-8d96-11e9-9e98-2ed5b8567510.PNG)<br>





* build.gradle(Module: app)

  Google Maps Android API 라이브러리 추가

  >  implementation 'com.google.android.gms:play-services-maps:16.1.0'<br>
     implementation 'com.google.android.gms:play-services-location:16.0.0'

  >  implementation 'com.android.support:appcompat-v7:28.0.0'<br>
     implementation 'com.android.support:support-media-compat:28.0.0'<br>
     implementation 'com.android.support:support-v4:28.0.0'

  Android-Google-Places-API 라이브러리 추가
  >  implementation 'com.google.android.gms:play-services-places:16.1.0'<br>
     implementation 'noman.placesapi:placesAPI:1.1.3'

  Sync Now를 클릭해준다. 다음과 같은 오류가 생길 것이다.
  >  Manifest merger failed : Attribute       
     application@allowBackup value=(true) from AndroidManifest.xml:8:9-35
	 is also present at [noman.placesapi:placesAPI:1.1.3] AndroidManifest.xml:12:9-36 value=(false).
	 Suggestion: add 'tools:replace="android:allowBackup"' to <application> element at AndroidManifest.xml:7:5-32:19 to override.
 
* AndroidManifest.xml에  추가해준다.

  AndroidManifest.xml 에서 application 태그의 allowBackup 속성을 false로 수정하면 위에 오류가 해결됩니다.<br>
  ![mn1](https://user-images.githubusercontent.com/48506075/59376811-d8df6380-8d8b-11e9-99a6-55ad7355ef6f.PNG)

  위치 정보를 사용하려면 권한을 추가해야 합니다.<br>
  ![mn2](https://user-images.githubusercontent.com/48506075/59377280-d3364d80-8d8c-11e9-9513-21433c65465f.PNG)<br>
  apache에서 제공하는 http 라이브러리가 최신 버전에서는 빠져있어 추가해주고 meta-data 태그에서 아까 발급받은 api 키를 써야지 작동됩니다.<br>
  ![mn3](https://user-images.githubusercontent.com/48506075/59377413-29a38c00-8d8d-11e9-9b06-d513bf2a9441.PNG)



* 구글맵 화면(activity_maps.xml).<br>


    ![1](https://user-images.githubusercontent.com/48506075/59374050-eabe0800-8d85-11e9-9b71-7c4750740a46.png)   
    ![4](https://user-images.githubusercontent.com/48506075/59400496-92612780-8dd2-11e9-875c-518824427b27.png) 


* MapsActivity.java 설명<br>

    ![캡처](https://user-images.githubusercontent.com/48506075/59382453-b99b0300-8d98-11e9-98cb-22531d09d127.PNG)<br>

    현재 위치를 얻고 여러가지 위치 정보 제공되는 코드<br>
    ![캡처2](https://user-images.githubusercontent.com/48506075/59384249-b86bd500-8d9c-11e9-9f4a-d4b80be8e512.PNG)<br>
    
   
    
    	//주변 가게 찾기 버튼(onCreate)
        Button btnSearch2 = (Button) findViewById(R.id.btnSearch2);
        btnSearch2.setOnClickListener(new Button.OnClickListener() {
            @Override
            public void onClick(View v) {
                prepareMap();
                drawMap();
                showPlaceInformation(currentPosition);
            }
        });



        private void drawMap() {
            //퍼미션 체크
            if (ActivityCompat.checkSelfPermission
                    (this, Manifest.permission.ACCESS_FINE_LOCATION//자세한 위치정보
                    ) != PackageManager.PERMISSION_GRANTED
                    && ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_COARSE_LOCATION)//대략적인 위치정보
                    != PackageManager.PERMISSION_GRANTED) {
                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.ACCESS_FINE_LOCATION, Manifest.permission.ACCESS_COARSE_LOCATION},
                        1);
                return;
            }
            if (currentPosition == null) {
                // 마지막 위치 정보 (최근에 위치한 장소)
                fusedLocationProviderClient.getLastLocation().addOnSuccessListener(this, new OnSuccessListener<Location>() {
                    @Override
                    public void onSuccess(Location location) {
                        if (location != null) {
                            mMap.setMapType(GoogleMap.MAP_TYPE_NORMAL);//일반지도
                            mMap.setMyLocationEnabled(true);//현재 위치 버튼
                            mMap.getUiSettings().setZoomControlsEnabled(true);//줌 컨트롤

                            LatLng myLocation = new LatLng(location.getLatitude(), location.getLongitude());
                            mMap.addMarker(new MarkerOptions()
                                    .position(myLocation)
                                    .title("현재 위치"));
                            mMap.moveCamera(CameraUpdateFactory.newLatLng(myLocation));
                            mMap.animateCamera(CameraUpdateFactory.newLatLngZoom(myLocation,15.0f));

                            //반경 1km원
                            CircleOptions circleOptions = new CircleOptions().center(myLocation)
                                    .radius(1000)     //반지름 단위 : m
                                    .strokeWidth(0f)  //선너비 0f : 선없음
                                    .fillColor(Color.parseColor("#8800005A")  //배경색
                                    );
                            //원추가
                            mMap.addCircle(circleOptions);
                        }

                    }
                });
            }else {
                //현재 좌표로 카메라 이동
                mMap.moveCamera(CameraUpdateFactory.newLatLng(currentPosition));
                //카메라 이동의 애니메이션 효과
                //줌레벨 : 1 ~ 21 숫자가 클수록 자세한 지도
                mMap.animateCamera(CameraUpdateFactory.newLatLngZoom(currentPosition, 13));
            }

        }  



        private void prepareMap() {
            int check = ContextCompat.checkSelfPermission(
                    this, Manifest.permission.ACCESS_COARSE_LOCATION);
            if(check != PackageManager.PERMISSION_GRANTED){
                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.ACCESS_COARSE_LOCATION},
                        1);
            }else {
                mMap.setMapType(GoogleMap.MAP_TYPE_NORMAL);//일반지도
                mMap.setMyLocationEnabled(true);//현재 위치 버튼
                mMap.getUiSettings().setZoomControlsEnabled(true);//줌 컨트롤

                //위치정보 관리자 객체
                LocationManager locationManager =
                        (LocationManager) getSystemService(Context.LOCATION_SERVICE);

                //리스너 등록
                locationManager.requestLocationUpdates(//리스너 등록
                        LocationManager.NETWORK_PROVIDER,0,
                        0,this);
                locationManager.requestLocationUpdates(//GPS 값이 바뀌면 감지하는 리스너
                        LocationManager.GPS_PROVIDER, 0,0,this);

                //수동으로 위치 구하기(최근에 방문했던 장소를 보여줌)
                String locationProvider = LocationManager.GPS_PROVIDER;
                Location lastLocation =
                        locationManager.getLastKnownLocation(locationProvider);

                //최근에 방문한 장소 gps 좌표를 저장
                if (lastLocation != null){
                    lat = lastLocation.getLatitude();
                    lng = lastLocation.getLongitude();
                }

                currentPosition = new LatLng(lat, lng);//현재좌표
            }
        }

        //장소 검색 함수
        private void showPlaceInformation(LatLng location) {
            mMap.clear();//기존 지도 지우기
            if (prevMarkers != null) {
                prevMarkers.clear(); // 기존에 표시됐던 마커 지우기
            }
            //구글 장소 검색 API 호출
            new NRPlaces.Builder()
                    .listener(this)
                    .key("") //장소 검색 api 키 값
                    .latlng(lat, lng) //현재 위치 기준
                    .radius(5000) //반경 5키로 이내 검색
                    .type(PlaceType.SHOE_STORE) //신발 가게
                    .build()
                    .execute();
            //서버에서 결과가 도착하면 onPlacesSuccess()가 호출됨.
        }

        //서버에서 장소 검색 결과가 도착하면 호출
        @Override
        public void onPlacesSuccess(final List<Place> places) {
            //매인 화면을 수정해야 하므로 runOnUiThread()에서 처리
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    //서버에서 조회된 장소들을 마커 리스트에 등록
                    for(Place place : places){
                        LatLng latLng = new LatLng(place.getLatitude(),
                                place.getLongitude());
                        MarkerOptions markerOptions = new MarkerOptions();
                        markerOptions
                                .position(latLng)
                                .title(place.getName())
                                .snippet(place.getVicinity());
                        Marker item = mMap.addMarker(markerOptions);
                        prevMarkers.add(item);

                    }
                    //중복된 값들을 제거하기 위해 HashSet 사용
                    HashSet<Marker> hashSet = new HashSet<>();
                    hashSet.addAll(prevMarkers);
                    prevMarkers.clear();
                    prevMarkers.addAll(hashSet);
                }
            });

        }
    
        

        //위치가 변경되면
        @Override
        public void onLocationChanged(Location location) {
            lat = location.getLatitude(); //변경된 위도
            lng = location.getLongitude(); //변경된 경도
            //새로운 현재 좌표
            currentPosition = new LatLng(lat, lng);
        }

        //지오 코딩
        public void search(View view) {
            String place = editPlace.getText().toString();


            Geocoder coder = new Geocoder(getApplicationContext());//텍스트를 읽어서 위도와 경도로 계산해서 지도를 요청한다.
            List<Address> list = null;
            try {
                list = coder.getFromLocationName(place, 1);
            } catch (IOException e) {
                e.printStackTrace();
            }
            Address address = list.get(0);
            double lat = address.getLatitude();//위도
            double lng = address.getLongitude();//경도
            LatLng geoPoint = new LatLng(lat, lng);//좌표 객체
            mMap.animateCamera(CameraUpdateFactory.newLatLngZoom(geoPoint, 15));

            //Marker 추가
            MarkerOptions markerOptions = new MarkerOptions()
                    .position(geoPoint)
                    .title(place)
                    .snippet(geoPoint.toString());
            mMap.addMarker(markerOptions);
        }

        @Override
        public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
            super.onRequestPermissionsResult(requestCode, permissions, grantResults);
            switch (requestCode){
                case 1:
                    if (ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)//자세한 위치정보
                        != PackageManager.PERMISSION_GRANTED
                        && ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_COARSE_LOCATION)//대락적인 위치정보
                        != PackageManager.PERMISSION_GRANTED) {
                        Toast.makeText(this, "권한 거부 됨", Toast.LENGTH_SHORT).show();
                    }
                    else{
                        drawMap();
                        prepareMap();
                    }
            }
        }

# 7. 프로젝트 소감 

### 신발 치수 재기 기능을 끝내 성공 시키지 못하여 많이 아쉬움이 남지만 프로젝트 제출 기간은 끝이 났어도 팀원들과 함께 신발 치수 재기 기능을 완성 시키고 싶다. -임대근-
### 여러모로 새로운 도전이었습니다. 끝나지 않을 것 같던 이 프로젝트도 마지막이라고 하니까 열심히 하지 못하고 대충 한 게 후회가 돼요. 너무 값진 경험이었습니다. -곽우석-
### 구글맵에 더 다양한 기능을 사용하지 못하고 끝나 아쉬운 점을 더 공부하여 완성도 있는 결과물을 만들고 싶었다. -장지희-

