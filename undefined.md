# 구글 클라우드 콘솔 설정

구글 클라우드 콘솔에서 프로젝트를 생성하는 방법을 살펴본다.

## 프로젝트 생성

대시보드에서 '프로젝트 만들기' 링크를 클릭한다.

![](<.gitbook/assets/image (44).png>)

프로젝트 이름을 입력하고 '만들기' 버튼을 클릭한다.

![](<.gitbook/assets/image (59).png>)

프로젝트가 생성되면 '알림' 레이어를 표시하고 대시 보드가 변경된다. 

![](<.gitbook/assets/image (24).png>)



[Google Cloud Console](https://console.cloud.google.com)

## API 사용 설정

구글 클라우드 API를 사용하려면 사용하려는 API에 대한 사용 설정을 해야 한다. "API 및 서비스>라이브러리"를 선택한다.

![](<.gitbook/assets/image (48).png>)



Google Workspace의 '모두보기(18개)'를 클릭한다. 

![](<.gitbook/assets/image (19).png>)

이 튜터리얼에서는 Google Drive API를 선택할 것이다. Google Drive API를 클릭한다.

\


![](<.gitbook/assets/image (46).png>)

'사용' 버튼을 클릭한다. 위에서 설명한 방법대로 사용하려고 하는 모든 API들은 모두 활성화한다.



> 구글 Map과 관련된 API를 사용하고 싶었는데 유료로 변경되었는지 무료 정보가 없었다. 더 확인을 해 봐야 할 것 같다.

## OAuth 동의 화면 구성

구글 클라우드 API를 사용하려면 사용자가 직접 인증을 해야 하기 때문에 OAuth 방식으로 구현해야 한다. OAuth를 구성하는 방법을 알아 보자.

### OAuth 동의 화면

사용자가 OAuth로 로그인할 때 '동의화면'이 표시되는데 이 때 사용할 동의화면에 대한 설정을 한다.

'API 및 서비스 > OAuth 동의 화면'을 클릭한다.



![](<.gitbook/assets/image (38).png>)



#### User Type 선택

G Suite(Workspace) 조직내의 사용자만이 사용하는 경우에는 "내부"를 선택하고 Google 계정이 있는 모든 사용자가 사용할 수 있도록 하려면 "외부"를 선택한다.

![](<.gitbook/assets/image (39).png>)



'만들기' 버튼을 클릭한다.

'앱이름'을 입력한다. '사용자 지원 이메일'을 입력한다. 



![](<.gitbook/assets/image (23).png>)



개발자 이메일 정보를 입력한다. 



![](<.gitbook/assets/image (31).png>)



'저장 후 계속' 버튼을 클릭한다.

#### 범위 추가

범위는 클라이언트 앱이 사용할 수 있는 API의 범위를 제한하는데 사용할 수 있다. 예를들어 클라이언트 앱에 발급된 엑세스 토큰에는 보호된 리소스에 대한 READ 및 WRITE 액세스 권한만 부여될 수 있다. API를 구현하여 원하는 모든 범위 또는 범위 조합을 적용할 수 있다. 따라서 클라이언트가 READ 범위를 가지는 토큰을 받아 WRITE 액세스를 필요로 하는 API .엔드 포인트를 호출하려고 시도하면 호출이 실패한다. 이제 이 앱에서 사용할 API의 범위를 설정해야 한다. "범위 추가 또는 삭제" 버튼을 클릭한다



![](<.gitbook/assets/image (6).png>)



'필터' 부분에 범위를 선택할 API를 입력한다.

![](<.gitbook/assets/image (11).png>)



Drive를 입력하면 Google Drive API와 관련된 선택할 수 있는 범위들이 표시된다. 



![](<.gitbook/assets/image (40).png>)



앱에서 사용할 피룡한 범위들을 선택한다. 

![](<.gitbook/assets/image (18).png>)





하단에 보면 '업데이트' 버튼이 보인다. 클릭한다. 

![](<.gitbook/assets/image (26).png>)





'업데이트' 버튼을 클릭하면 '민감한 범위' 및 '민감하지 않은 범위' 등의 목록이 화면에 표시된다. 범위는 나중에라도 변경할 수 있다.

맨 아래에 '저장 후 계속' 버튼을 클릭한다. ' 테스트 사용자' 화면이 표시된다. 이 부분은 건너 뛰자. '저장 후 계속' 버튼을 클릭한다.



![](<.gitbook/assets/image (27).png>)



요약 화면이 표시된다. 모두 완료 되었다. 



![](<.gitbook/assets/image (42).png>)
