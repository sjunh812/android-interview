# 🎙 Android Interview
안드로이드 신입 개발자 면접을 위한 간단한 개념 및 질문 정리  
<br>  

## 목차
1. [Android](#Android)
2. [Kotlin](#Kotlin)
3. [CS](#CS)
<br>

## Android
### 1. Android 4대 컴포넌트 
안드로이드는 4개의 컴포넌트로 구성되어 있음. (`Activity`, `Service`, `Broadcast Receiver`, `Content Provider`)
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
  * `onStop()` 이후 해당 액티비티로 다시 돌아올 경우, `onRestart()` → `onStart()` → `onResume()` 순서로 Lifecycle 실행
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

### 8. Process Lifecycle
안드로이드는 프로세스를 가능한 오랫동안 유지하려고 하지만,  
새로운 프로세스를 생성하거나, 우선순위가 높은 프로세스의 메모리를 확보하기 위해  
다른 프로세스를 종료시키는 경우가 있음
1. **Foreground Process** : 현재 조작하는 일에 대한 프로세스
2. **Visible Process** : Foreground 상태에 놓여있지는 않지만, 사용자 화면에는 보이는 프로세스 (ex) 다이얼로그가 띄워진 액티비티)  
3. **Service Process** : 서비스가 실행되는 프로세스 (사용자가 하고 있는 일에 영향)
4. **Background Process** : `Activity` 는 있으나, `onStop()` 이 불린 이후여서, 더이상 사용자에게 보이지 않는 프로세스
5. **Empty Process** : **Activity Componet** 를 갖고 있지 않는 프로세스 (다음 재실행 시, 걸리는 시간을 줄이기 위해 캐싱된 프로세스)

### 9. SharedPreferences
안드로이드에서 사용할 수 있는 데이터 저장소  
데이터를 **XML** 파일에 저장  
데이터를 저장한 파일은 앱 폴더 내에 저장되므로, 앱이 삭제되면 데이터도 함께 삭제 

### 10. Intent 와 Bundle
인텐트는 데이터를 전달하는 수단의 객체  
번들은 데이터를 저장하기 위한 객체

### 11. Android Architecture
안드로이드 아키텍처는 4가지의 **key component** 로 이루어져 있음
1. **Linux Kernel** : 메모리 관리, 보안 설정, 네트워크 시스템 관리를 담당
2. **Libraries and Runtime** : 안드로이드 기능 라이브러리와 가상머신의 역할  
모바일 데이터베이스, 그래픽을 담당
3. **Android Framework** : 생명주기, 환경설정 등의 역할 (GPS, 리소스 관리)
4. **Android Application** : 안드로이드에서 기본적으로 제공하는 역할 (전화걸기, 브라우저)

### 12. Android Manifest
매니페스트는 안드로이드 프로그램에서 필수적이며,  
코드를 실행하기 전에 안드로이드 시스템이 알아야하는 애플리케이션에 대한 정보를 포함하는 곳 (앱 이름, 컴포넌트 정보 등)  

### 13. OkHttp Interceptor
`Retorfit` 은 내부적으로 `OkHttp` 라이브러리를 이용하여 네트워크 통신을 구현  
**OkHttp Interceptor** 는 **애플리케이션** 과 **OkHttp 코어** 사이의 **요청/응답** 을 가로채는 역할을 함 

### 14. Vector 와 Bitmap
- Vector : 리사이징 되어도 깨지지 않음. 모든 해상도에서 자유자재로 활용 가능 (ex) SVG)
- Bitmap : 픽셀로 구성되어 있으며, 해상도에 따라 깨질 수 있음 (ex) PNG, JPEG)

### 15. Android Jetpack
안드로이드 앱을 구축하는데 도움이 되는 훌륭한 도구 모음  
즉, Jetpack 은 안드로이드 개발자들이 더욱 쉽게 높은 퀄리티의 앱을 개발할 수 있도록 도와주는 라이브러리들의 모음집  
(ex) `Databinding`, `Room`, `Navigation`, `Paging`, `Lifecycles`, `LiveData`)

### 16. JAR, AAR, DEX, APK
- **JAR** (Java Archive) : 해당 플랫폼에서 `Java` 응용 프로그램을 배포하기 위해 고안된 패키지 파일 형식 (클래스 파일, 매니페스트 파일이 포함)
- **AAR** (Android Archive) : 안드로이드 라이브러리 프로젝트의 바이너리 배포판 (리소스 파일 포함)
- **DEX** (Dalvik Excutable) : DVM(Dalvik Virtual Machine)을 위한 실행 파일  
Android SDK 의 DEX 컴파일러에 의해 JVM 바이트 코드를 DVM 바이트 코드로 변환하고, 모든 class 파일을 DEX 파일에 넣음
- **APK** (Android Application Package) : 안드로이드 플랫폼에 배포할 수 있도록 설계된 파일 

### 17. Application class
안드로이드 기본 클래스로, 안드로이드 앱에 대한 모든 컴포넌트, `Activity` 와 `Service` 를 포함하고 있는 클래스  
응용 프로그램/패키지에 대한 프로세스가 생성될 때, 다른 클래스보다 먼저 인스턴트화   

### 18. String, StringBuffer, StringBuilder
- `String` : 불변, 문자를 수정하려면 새로운 객체를 생성해야 함
- `StringBuffer` : 가변, 한번 만들고, 필요에 따라 크기를 변경하여 문자를 변경 (`append()` 와 같이)
- `StringBuilder` : `StringBuffer` 와 유사하나, **동기화를 지원하지 않아 멀티 스레드 환경에 부적합**
<br>

## Kotlin
### 1. Scope Function
- `apply` : 생성과 동시에 초기화, 자기 자신 return
- `also` : 수신 객체를 명시적으로 사용하고, 자기 자신 return (ex) 로그)
- `with` : 생성과 동시에 초기화, 특정한 값 return
- `run` : 객체의 값에 쉽게 접근하고, 특정한 값 return
- `let` : 수신 객체를 명시적으로 사용 (ex) null 체크)

### 2. 초기화 지연
변수를 선언할 때, 값을 저장하지 않고, 나중에 저장할 수 있는 방법  
메모리를 효율적으로 사용하기 위해, 그리고 **null-safe** 한 value 를 사용하기 위해 사용됨
- `lateinit`
  - `var` (mutable) 를 사용
  - **primitive** 타입을 사용할 수 없음 (ex) `Int`)
  - 선언 후, 나중에 초기화 해줘도 됨
  - 변수 타입을 반드시 지정해줘야 함 (ex) lateinit var name: String)
- `by lazy` 
  - `val` (immutable) 를 사용
  - 선언과 동시에 초기화 필요
  - 호출되는 시점에서 실질적인 초기화가 이루어짐 (메모리룰 효율적으로 사용) 
  - ex) val age by lazy { 10 }

### 3. 동등성과 동일성
- 동등성 (equality) : 두 객체의 값이 같은지 비교, 값을 비교하며, 내부적으로 `equal()` 호출 (`==`)
- 동일성 (identity) : 두 객체가 같은 주소를 참조하는지 비교, 주소값을 비교하며, 식별자를 기반으로 객체 판단 (`===`)

### 4. data class 에서 copy()를 사용하는 이유? data class 를 왜 불변으로 권장하는지?
`copy()` 를 사용하면, 복사를 하여 일부 프로퍼티를 바꾸거나, 복사본을 삭제해도 프로그램에서 원본을 참조하는 다른 부분에 전혀 영향이 없음  

data class 를 키로 하는 컨테이너를 만들고, 키로 쓰인 data class 의 프로퍼티를 변경하면, 컨테이너 상태에 문제가 생길 수 있음 → 불변 권장  
멀티 스레드의 경우 스레드가 사용 중인 data class 를 다른 스레드에서 변경할 수 없으므로 **동기화** 가 필요 없게 됨

### 5. 중첩 클래스와 내부 클래스 차이
바깥쪽 클래스에 대한 참조를 저장하는지, 안하는지 차이  
(중첩 클래스 : class A (static), 내부 클래스 : inner class B)

### 6. Companion object
클래스가 메모리에 적재되면서, 함께 생성되는 객체 (`Java` 의 **static** 과 유사)  
static 과 다르게, companion object 는 변수로 할당 가능하고, 할당된 변수를 통해 멤버를 참조할 수 있음  
<br>  

## CS
### 1. Singleton
싱글톤 패턴은 특정 클래스에 대한 인스턴스를 **단 한번만** static 영역의 메모리에 할당하고, 해당 클래스에 대한 생성자를 여러번 호출 하더라도,  
최초에 생성된 객체를 반환하는 디자인 패턴  
**즉, 애플리케이션의 유일한 객체를 보장하는 디자인 패턴**  
#### 장점
- 고정된 메모리 영역을 얻으면서, 한 번의 new 인스턴트를 생성하여 사용하기 때문에 메모리 낭비 방지
- 전역 인스턴트 때문에 공유가 쉬움
#### 단점
- 싱글톤 인스턴트를 너무 많이 사용하거나, 많은 데이터를 공유시킬 경우, **결합도** 가 높아져 **개방 폐쇠 원칙** 에 위배  
(객체지향 설계 원칙에 어긋)
- 동기화 처리를 안하면, 인스턴트가 두 개 생성되는 문제 발생

### 2. MVC, MVP, MVVM
#### MVC (Model, View, Controller)
안드로이드에서는 Controller 를 따로 나눌 수 없기 때문에, View 와 Controller 의 하는 일을 `Activity` 혹은 `Fragment` 에서 하게 됨
- 장점
  - 코드만 읽을 수 있다면, 다른 패턴에 비해 쉽게 해석 가능
  - 개발 기간이 짧을 수 있음
- 단점
  - 유닛 테스트가 어려움
  - 시간이 지남에 따라 코드가 길게 작성되어, 문제가 발생하기 쉬움
  - View 와 Model 의 결합도가 높음
#### MVP (Model, View, Presenter)
View 가 **수동적**, 기존 MVC 에서는 Model 데이터를 View 에서 직접 반영했다면, MVP 는 명령하는 주체인 **Presenter** 가 View 에게 데이터를 보여달라고 명령하는 형태
- 장점
  - View 와 Model 의 의존성이 없음
  - 새로운 기능 추가 및 변경사항이 있을 때, 관련된 부분만 수정하면 되므로, 확장성이 좋음
  - 테스트 코드의 작성이 편리
- 단점
  - MVC 에서는 View 에서 모든 데이터를 처리했다면, MVP 에서는 `View → Presenter → View → Presenter..` 와 같이 코드 작성
  - View 와 Presenter 는 **1:1** 관계이므로, View 1개에는 Presenter 1개가 무조건 있어야함  
  (View 와 Presenter 의 의존 관계가 강함)
#### MVVM (Model, View, ViewModel)
MVP 와 반대로 View 가 **능동적**, View 는 스스로 ViewModel 의 객체를 관찰함  
`LiveData`, `Observable`, `ObservableField` 등을 사용하여 관찰필드에 변화가 생기면, View 가 알림을 받고, 알맞는 View 랜더링 로직을 수행  
(`Databinding` 을 통해 View 와 ViewModel 사이의 일을 UI 코드로 작성하여, **View 와 ViewModel 의 독립성을 높일 수 있음**)
- 장점
  - 유닛 테스트에 용이
  - View 의 의존성이 없음
  - View 와 ViewModel 의 종속성이 **1:n** 으로 사용가능
- 단점
  - 사전에 알아야할 사항이 많음 (구조, Databinding, BindingAdapter)
  - 비교적 유지보수가 힘들 수 있음 (XML, ViewModel, BindingAdapter)

### 3. DI
DI (Dependency Injection) 은 **의존성 주입** 으로, 필요로 하는 객체를 직접 생성하지 않고, 외부로 부터 주입받는 기법을 의미
- Dependency (의존) : 함수에 필요한 클래스 또는 참조변수나 객체에 의존하는 것 
- Injection (주입) : 외부에서 객체를 생성해서 넣어주는 것 

### 4. 함수형 프로그래밍과 객체지향 프로그래밍
#### 프로그래밍 패러다임
- 명령형 프로그래밍
  - 절차지향 프로그래밍 : 수행해야 할 연속적인 계산 과정을 포함하는 프로그래밍
  - 객체지향 프로그래밍 : 객체들의 집합으로 프로그램의 상호작용을 표현 
- 선언형 프로그래밍
  - 함수형 프로그래밍 : 순수 함수를 조합하여 프로그램을 만드는 방식
#### 함수형과 객체지향의 차이
객체지향은 객체 안에 상태를 저장하고, 상태변화를 설정하고, 조정하기 위해 다양한 기능을 사용  
이에 반해 함수형은 상태를 제어하는 것보다, 상태를 저장하지 않고 없애는데 포인트

### 5. 직렬화, 역직렬화
#### 직렬화
메모리에 존재하는 정보(객체 또는 데이터)를 보다 쉽게 전달, 전송하기 위해 **byte** 형태로 데이터를 변환하는 기술  
(JVM 의 메모리에 상주되어 있는 객체 데이터를 바이트 형태로 변환하는 기술)
#### 역직렬화
byte 로 변환되어 있는 데이터를 원래대로 객체나 데이터로 변환하는 기술  
(직렬화된 바이트 형태의 데이터를 객체로 변환해서 JVM 에 상주시키는 형태)  
#### Serializable
- **Implement** (구현) 하는 것만으로 쉽게 직렬화를 할 수 있음
- **Reflection** 을 사용하여 직렬화를 처리하므로, 추가로 많은 객체가 생성되어 가비지 컬렉터의 표적이 되고, 성능이 문제로 이어질 수 있음  
(**Reflection** : run-time 에서 동적으로 클래스들의 정보를 알아내고 실행할 수 있는 것)
#### Parcelable
- 안드로이드에서 권장하는 직렬화 방법
- **Serializable** 이 했던 **Reflection** 을 사용하지 않도록 설계되어 있어, 개발자가 수동적으로 해야하는 작업이 있음  
→ Kotlin 의 `@Parcelize` 어노테이션을 통해 쉽게 구현

### 6. Process, Thread
#### Process
컴퓨터에서 연속적으로 실행되고 있는 프로그램  
프로세스는 운영체제로부터 시스템 자원을 할당 받는 작업의 단위 
#### Thread
운영체제로부터 자원을 할당 받은 프로세스 내에서 실행되는 최소 단위  
스레드에는 `start` 와 `run` 방식이 있음
- `start` : **JVM** 에서 스레드를 위한 call stack(stack 영역) 을 새로 만들기 때문에, 독립적으로 사용 가능
- `run` : 메인스레드에서 call stack 을 사용하기 때문에, `run` 메소드가 끝나기 전까지 다른 작업을 하지 못함
#### Muti Thread
프로그램의 흐림이 2개 이상인 것을 말함  
매우 빠른 시간 간격으로 **스위칭** 되기 때문에 동시에 실행되는 것처럼 보임 (**동시성**)  
- **Context Switching** : 하나의 프로세스가 CPU 를 사용 중인 상태에서 다른 프로세스가 CPU 를 사용하도록 하기 위해,  
이전 프로세스 상태를 보관하고, 새로운 프로세스의 상태를 적재하는 작업

### 7. Framework, Library
- Framework : 특정 프로그램을 개발하기 위한 여러 요소들과 메뉴얼인 룰을 제공하는 프로그램
- Library : 소프트웨어를 개발하기 쉽게 어떤 기능을 제공하는 도구  

**프레임워크는 꼭 써야하는 것과 지켜야하는 룰이 있지만, 라이브러리는 사용 여부를 개발자 마음대로 할 수 있음 (자유도의 차이)** 

