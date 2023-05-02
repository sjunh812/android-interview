# 🎙 Android Interview

## Android
### 1. Android 4대 컴포넌트 
안드로이드는 4개의 컴포넌트로 구성되어 있음.  
(`Activity`, `Service`, `Broadcast Receiver`, `Content Provider`)
- `Actvity` : **UI** 가 있어, 사용자와 직접적인 상호작용을 하는 컴포넌트
- `Service` : 백그라운드에서의 작업을 수행하는 컴포넌트
  - 포그라운드 서비스 : 알림(`Notification`)이 필요
  - 백그라운드 서비스 : **UI** 가 없음
  - 바인드 서비스 : 앱 내에서 서비스를 사용하여 간단한 **서버-클라이언트** 환경 구성
- `Broadcast Receiver` : 디바이스에서 발생하는 다양한 이벤트 및 정보를 받고 반응하는 컴포넌트
  - 정적 리시버 : **Manifest** 에 등록, 해제 불가능
  - 동적 리시버 : 클래스 파일에 동적으로 등록 및 해제 (적절히 해제하지 않을 경우 **메모리 누수** 발생)
- `Content Provider` : 데이터를 저장하고, 가져오며, 다른 앱에 접근할 수 있도록 하는 컴포넌트
  - 다른 앱의 데이터를 사용하기 위해 **URI** 를 이용하여, 콘텐츠 리졸버가 다른 앱의 콘텐츠 프로바이더에게 요청
  - 요청 받은 콘텐츠 프로바이더는 **URI** 를 확인하고, 데이터를 콘텐츠 리졸버에게 전달 

### 2. Activity 와 Fragment 차이
1. `Activity` 는 독립적으로 사용 가능
2. `Fragment` 는 `Activity` 에 종속
3. `Activity` 는 전체화면을 차지하나, `Fragment` 는 꼭 전체화면을 차지하지 않아도 됨

### 3. Activity, Fragment Lifecycle
- Activity Lifecycle : `onCreate()` → `onStart()` → `onResume()` → `onPause()` → `onStop()` → `onDestroy()`
  * `onPause()` 이후 해당 액티비티로 다시 돌아올 경우, `onResume()` 호출
  * `onStop()` 이후 해당 액티비티로 다시 돌아올 경우, `onRestart()` → `onStart() → `onResume()` 순서로 Lifecycle 실행
  * **configuration** 이 발생할 경우 `onCreate()` 부터 다시 실행
- Fragment Lifecycle : `onAttach()` → `onCreate()` → `onCreateView()` → `onActivityCreated()` → `onStart()` → `onResume()`  
→ `onPasue()` → `onStop()` → `onDestroyView()` → `onDestroy()` → `onDetach()`

### 4. Intent
인텐트는 컴포넌트 간에 정보를 주고 받을 수 있는 **Message Object**(메시징 객체) 이다.
* `PendingIntent` : 인텐트를 가지고 있는 클래스로, 다른 앱의 권한을 허용하여 가지고 있는 인텐트를 마치 본인 앱에서 실행하는 것처럼 사용하는 것

### 5. ANR
**ANR(Application Not Responding)** 은 안드로이드 앱의 **메인 스레드(UI 스레드)** 가 오랫동안 차단되면 발생하는 오류 

### 6. Annotation
**Annotation** 은 주석의 의미를 가지고 있으며,  
특정 클래스, 변수, 메소드 등에 붙이는 코드로 해당 타겟의 기능을 좀 더 명확하게 해주는 역할  

### 7. Context
컨텍스트는 여러 컴포넌트의 상위 클래스  
안드로이드 시스템은 애플리케이션 또는 컴포넌트를 컨텍스트로 관리 (리눅스의 프로세스 ID 와 유사)
