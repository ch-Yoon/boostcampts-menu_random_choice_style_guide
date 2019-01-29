이곳에 정의된 내용이 아닌 케이스가 발생될 경우, 팀원과 협의한 후 이곳에 작성한다.

# Java

#### 함수 작성 순서는 다음과 같은 순서로 작성한다.
- `생명주기 함수` -> `초기화 함수` -> `override 함수` -> `public 함수` -> `private 함수`
    
#### 이름 명명 규칙은 다음을 따른다.
- 클래스명은 대문자로 시작하는 카멜 케이스로 작성한다 : `MovieManager`
- 변수명은 소문자로 시작하는 카멜 케이스로 작성한다 : `leftOfRect`
- 패키지명은 모두 소문자로 작성한다 : `utils`
- 상수 선언은 대문자 스네이크 케이스로 작성한다 : `NETWORK_NOT_CONNECT`
- 함수명의 시작은 동사로 시작한다 : `public void requestMovieData()`
- 약자는 카멜 케이스를 적용하지 않는다 : `naverApiKey -> X`, `naverAPIKey -> o`
- check 함수명은 긍정문을 사용한다 : `isPlaying`
    
#### 함수 작성 규칙은 다음을 따른다.
- Context류의 parameter를 가장 앞에 위치한다 : `void loadMovieData(Context context, String moveTitle);`
- Callback류의 parameter를 가장 뒤에 위치한다 : `void requestMoreMovieData(Context context, Listener listener);`
    
#### Key-Value를 위한 Key는 다음 규칙을 따른다.
- Intent는 EXTRA, SharedPreferences는 PREF, Argument는 ARGUMENT로 시작한다.
- key와 value는 동일하게 작성한다.
- `public static final String EXTRA_NAME = "EXTRA_NAME";`
- `public static final String PREF_LOGIN_TOKEN = "PREF_LOGIN_TOKEN";`
    
#### Fragment
- Fragment에 ARGUMENT_를 넣어주는 경우, 해당 Fragment에 newInstance()를 구현하고 이를 사용한다.
- Fragment 생성자의 Parameter로 넘기지 않는다.    
public static UserFragment newInstance(User user) {    
&nbsp;&nbsp;&nbsp;&nbsp;UserFragment fragment = new UserFragment();            
&nbsp;&nbsp;&nbsp;&nbsp;Bundle args = new Bundle();    
&nbsp;&nbsp;&nbsp;&nbsp;args.putParcelable(ARGUMENT_USER, user);    
&nbsp;&nbsp;&nbsp;&nbsp;fragment.setArguments(args)    
&nbsp;&nbsp;&nbsp;&nbsp;return fragment;    
}



#### Line
- 1줄에 100자를 넘지 않도록 작성한다.
- 코드간의 간격은 2줄이상 간격이 발생하지 않도록 한다.(최대 1줄 줄바꿈)

- Parameter
Parameter개수가 많아서 줄바꿈이 필요한 경우, `,`다음부터 줄바꿈한다.    
public InputSingleTextView(Context context,      
&nbsp;&nbsp;&nbsp;&nbsp;@RegisterStep String step,    
&nbsp;&nbsp;&nbsp;&nbsp;String hint,    
&nbsp;&nbsp;&nbsp;&nbsp;String validationMessage,    
&nbsp;&nbsp;&nbsp;&nbsp;@NonNull CompleteListener completeListener) {      
&nbsp;&nbsp;&nbsp;&nbsp;...    
}     


- 줄바꿈이 필요한 부분부터 줄바꿈 하지 않고 위의 예시처럼 1개 단위로 줄바꿈을 해준다. 호출코드에서도 동일.
new InputSingleTextView(this,    
&nbsp;&nbsp;&nbsp;&nbsp;RegisterStep.XXX,    
&nbsp;&nbsp;&nbsp;&nbsp;getString(R.string.xxx),    
&nbsp;&nbsp;&nbsp;&nbsp;getString(R.string.xxx),    
&nbsp;&nbsp;&nbsp;&nbsp;completeListener);
   
- Operator
많은 operator의 연산으로 줄바꿈이 필요한 경우, operator 전에 줄바꿈한다.    
int longName = anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne    
        + theFinalOne;     
연산자의 경우는 줄바꿈이 필요한 위치부터 줄바꿈한다.    


- Method chain
Builder/RxJava 등 여러 함수를 chaining으로 사용하면서 줄바꿈이 필요한 경우, .전에 줄바꿈한다.    
ImageLoader.load(user.getProfileUrl())      
        .placeholder(R.drawable.img_user_placeholder)      
        .fitCenter()      
        .into(binding.ivUser);    
   

#### 새파일 생성시 주석
새로운 파일을 만들때 자동으로 만들어지는 주석은 만들지 않는다.    
예)    
`수정방법: Preferences -> Editor -> File and Code Templates -> includes탭 -> File Header 내용 삭제`

#### Annotation    
외부에서 호출할 수 있는 public 함수에서는 항상 @NonNull / @Nullable 어노테이션을 추가해준다.    
public RegisterStepManager(@NonNull RegisterContract.View view,    
&nbsp;&nbsp;&nbsp;&nbsp;@NonNull Activity activity,    
&nbsp;&nbsp;&nbsp;&nbsp;@NonNull RegisterContract.Presenter presenter,    
&nbsp;&nbsp;&nbsp;&nbsp;@NonNull ActivityRegisterBinding binding,    
&nbsp;&nbsp;&nbsp;&nbsp;@NonNull String registerHashId) {    
&nbsp;&nbsp;&nbsp;&nbsp;this.view = view;    
&nbsp;&nbsp;&nbsp;&nbsp;this.activity = activity;     
&nbsp;&nbsp;&nbsp;&nbsp;this.presenter = presenter;     
&nbsp;&nbsp;&nbsp;&nbsp;this.binding = binding;     
&nbsp;&nbsp;&nbsp;&nbsp;this.registerHashId.set(registerHashId);     
&nbsp;&nbsp;&nbsp;&nbsp;binding.setIsLoading(isLoading);     
&nbsp;&nbsp;&nbsp;&nbsp;setMessageRecyclerView();     
&nbsp;&nbsp;&nbsp;&nbsp;setListener();    
}     
    
#### Util   
public static void AAA등으로 쓰이는 여러곳에서 사용되는 util성 기능을 보아둔 클래스   
aa.bb.cc.util 패키지에 모두 모아둔다.    
예) DateFormatUtil, PixelUtil, BitmapUtil등   

#### Manager    
항상 내부에서 instance로 만들어서 관리되는 용도    
내부적으로 state 혹은 information을 가지고 있어서 호출한곳에서의 상태에 따라서 관리되는 값을 변경하고 반영하는 작업을 해준다.    
예) RegisterStepManager, RegisterCarInfoConfirmManager등    


#### if문    
if (isChecked == false) 와 같은 코드는 명백한 Lint warning이므로 사용하지 않는다.    
if (isUnchekced)    
조건문에 !를 넣는것대신 아래와 같은 규칙으로 코드를 작성한다.    
조건문에서 체크되는 boolean 변수/함수는 항상 긍정문으로 작성한다. if(isChecked())    
한줄의 조건문이어도 중괄호는 반드시 사용한다.    

#### Layout
`<WHAT>_<WHERE>`    
WHAT    
Prefix	설명    
activity_	Activity에서 쓰이는 layout    
fragment_	Fragment에서 쓰이는 layout    
dialog_	Dialog에서 쓰이는 layout    
view_	CustomView에서 쓰이는 layout    
item_	RecyclerView, GridView, ListView등에서 ViewHolder에 쓰이는 layout    
layout_	<include/>로 재사용되는 공통의 layout    

- 예시    
`activity_main`: MainActivity의 layout    
`fragment_request`: RequestFragment의 layout    
`dialog_contact`: 문의안내 Dialog의 layout    
`view_rating`: 커스텀으로 만든 RatingView의 layout    
`item_my_car`: 내차량 목록에서 사용되는 각각의 item의 layout    
`layout_dealer_review`: 재사용되는 딜러리뷰 layout    

#### string
`<WHERE>_<DESCRIPTION>`    
- 예시    
`activity_main_movie_title`: activity_main layout에서 사용되는 movie title text    
`all_movie_title`: 다른 곳에서도 사용될 수 있는 movie title text
