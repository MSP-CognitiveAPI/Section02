# Section02
Cog.io Section02

##Cogio YoutubeScript project
Cogio 유튜브 스크립트 프로젝트는 YoutubeExtractor dll과 Azure Cognitive service를 이용한 프로젝트 입니다.

##YoutubeExtractor
 - Overview
 YoutubeExtractor는 .NET용 라이브러리이며, C#으로 작성되어 있고 유튜브에서 비디오를 다운로드 할 수 있고 오디오 트랙을 추출할 수 있습니다. (현재는 플래시 비디오에서만 오디오 추출이 가능합니다.)

 ![alt tag](https://github.com/cog-io/Section02/blob/master/picture/KakaoTalk_Photo_2016-11-11-19-35-54_11.jpeg)

##Azure Cognitive service

### Bing Speech API

 ![alt tag](https://github.com/cog-io/Section02/blob/master/picture/KakaoTalk_Photo_2016-11-11-19-42-44.jpeg)

 Bing speech API는 음성을 텍스트로 변환하고 다시 음성으로 변환하여 의도를 이해합니다.

 - 음성 인식
 파일의 오디오나 마이크 또는 기타 오디오 소스의 라이브 음성을 포함한 음성 오디오를 실시간으로 텍스트로 변환합니다. 또한 실시간 스트리밍이 가능하므로 오디오가 서버로 전송될 때 부분 인식 결과도 반환됩니다.

 - 음성 의도 인식
 음성 오디오를 작업을 유도하는 의도로 변환합니다. 음성 의도 인식은 언어 인식 인텔리전트 서비스 모델을 사용하여 응용 프로그램이 음성을 텍스트로 변환할 뿐만 아니라 말하는 사람의 의도를 손쉽게 파악하여 앱 내에서 “알람 설정”과 같은 작업을 만들 수 있도록 해줍니다.

 - 텍스트 음성 변환
 텍스트를 음성 오디오로 변환합니다. 응용 프로그램이 사용자에게 다시 “말”해야 할 경우 이 API가 앱에서 생성된 텍스트를 사용자에게 재생 가능한 오디오로 변환합니다.

###Translator speech API

![alt tag](https://github.com/cog-io/Section02/blob/master/picture/KakaoTalk_Photo_2016-11-11-19-42-26.jpeg)

Microsoft Translator Speech API는 클라우드 기반 automatic translation(자동 번역) 서비스입니다. 개발자는 이 API를 사용하여 응용 프로그램 또는 서비스에 종단 간 실시간 음성 번역을 추가할 수 있습니다.

- 응용 프로그램 도달 범위 확장
모바일, 데스크톱 및 웹 응용 프로그램 전체에서 클라우드 기반 자동 음성 번역 서비스(기계 번역이라고도 함)인 Translator Speech API의 개방형 REST 인터페이스를 통해 9개 언어로 번역 할 수 있습니다.

- 실제 대화 기록 및 번역
실제 대화의 번역에 최적화된 기술을 사용하여 음성 번역을 앱에 추가할 수 있습니다.

- 응용 프로그램 요구 사항에 맞게 조정
고유한 시나리오에 따라 API에서 사용 가능한 출력(말할 때 부분적인 기록, 부분적인 텍스트 번역, 최종 기록, 최종 텍스트 번역 또는 오디오 텍스트 음성 변환 번역)을 이용할 수 있습니다.






##Cogio YoutubeScript project Azure Cognitive 부분

###1. 초기 셋팅
![alt tag](https://github.com/cog-io/Section02/blob/master/picture/initialize.PNG)

- Azure Cognitive Speech api를 쓰기 위해서는 **DataRecognitionClient** 의 변수가 필요합니다.
 위의 화면에서는 m_dataClient라는 변수로 이를 이용합니다.
- speech api에서 화자의 음성을 인식하는 방법은 크게 2가지로 나뉩니다. 화자의 마이크 받은 데이터를 텍스트로 변 환하는 기술과 기존 음성파일에 있는 데이터를 텍스트로 바꾸는 기술을 들수 있습니다. YoutubeScript에서는 기존 음성파일의 데이터를 애저에 보내서 인식하는 과정을 거칩니다. **SpeechRecognitionMode** 에서 longDictation기능은 긴 음성 파일을 애저로 보내주는 매서드를 담당하고 있습니다.
- DefaultLocale은 애저서버로 음성파일을 보낼때 어떤 언어로 바꿀것인지 고르는 선택 배열입니다.
- primarykey는 애저서버에서 할당하는 accesstoken입니다.
- translate_SubscriptionKey는 애저서버에서 translator api를 쓸때 쓰는 토큰키입니다.

###2. 두번째 초기 셋팅 생성자
![alt tag](https://github.com/cog-io/Section02/blob/master/picture/2.PNG)

-  **DataRecognitionClient** 에서 변수로 받은 m_dataClient를 통해 애저와 연결하려면 **Speech
RecognitionServiceFactory.CreateDataClient** 메서드가 필요합니다. 이 메서드는 3개의 매개변수를 갖는데 앞서 지정한 longDictation을 지정한 m_recoMode, DefaultLocale에서 지정한 언어 , primarykey가 들어갑니다.

- Speech API를 이용할 때는 3개의 핸들러를 만들어야합니다. 이는 OnResponseReceived 과 OnPartialResponseReceived 와 OnConversationError핸들러를 들수 있습니다.

###3. Error 헨들러
![alt tag](https://github.com/cog-io/Section02/blob/master/picture/3(errorhandler).PNG)

- 이 헨들러는 애저와 클라이언트사이에 문제가 발생할 시 에러를 띄워주는 창입니다.
- 주로 키가 만료되거나 request가 잘못 될때 나타납니다.

###4. PartialResponseReceived 헨들러
![alt tag](https://github.com/cog-io/Section02/blob/master/picture/4(partialResponse).PNG)

- 이 헨들러는 애저와 부분 부분 request와 response를 주고 받을 때 생기는 값들을 저장합니다.
  실시간으로 Speech api가 분석하는 대로 response값을 e.PartialResult라는 변수에 저장합니다.

###5. OnResponseReceived 헨들러
![alt tag](https://github.com/cog-io/Section02/blob/master/picture/5(ResponseReceive).PNG)

- 이 헨들러에는 PartialResponseReceived에서 받은 response값중 가장 정확한 값들을 선별해 사용자에게 response하는 역할을 합니다.
- response값들을 모아서 System.IO.StreamWriter를 통해 text 파일로 저장하는 과정을 거칩니다.

###6. sendAudio 헨들러
![alt tag](https://github.com/cog-io/Section02/blob/master/picture/6(endAudio).PNG)

- sendAudio 메서드는 fileStream을 통해 wav파일을 애저서버에 전송하는 역할을 합니다.
- wav 파일외에 다른 형식을 올리려면 그에 맞는 형식에 대한 설정을 갖춰서 보내야합니다. YoutubeScript에서는 이 과정을 생략하고 wav파일로 올리는 작업을 합니다.

###7. YoutubeExtractor .dll
![alt tag](https://github.com/cog-io/Section02/blob/master/picture/7(Youtubeextractor).PNG)

**[관련 동영상 링크](https://www.youtube.com/watch?v=TnG3urCD_m0)**

- Youtube에서 동영상을 추출하기 위해서 이 프로그램에선 YoutubeExtractor.dll을 이용합니다. 먼저 추출할 동영상의 주소를 받는 작업을 DownloadUrlResolver.GetDownloadUrl에서 받아옵니다.
- video파일을 받을때 비디오 형식을 mp4로 해상도는 240,360,480p로 해상도 선택창에서 선택할수 있습니다.
- VideoDownloader에서 앞서 설정한 비디오 변수를 통해 mp4로 동영상을 호출합니다.

###8. Bing Translator 셋팅
![alt tag](https://github.com/cog-io/Section02/blob/master/picture/9(translatorClick).PNG)

**[관련 동영상 링크](https://www.youtube.com/watch?v=b8etXQB0Sy0)**

- bing Translator를 이용하기 위해선 request header양식을 맞춰주어야 합니다.
- 애저 홈페이지에서 ADMAccessToken을 제공받고 이를 headerValue에  "Bearer" 와 admToken.access_token으로 넣어야 합니다.

###9. Bing Translator TransformTextMethod
![alt tag](https://github.com/cog-io/Section02/blob/master/picture/11(TransformTextMethod).PNG)

- bing translator에서 번역을 하기위해선 httpWebRequest를 통한 서버통신을 이용합니다.
- uri 변수에 저장된 text와 바꾸고 싶은 언어를 설정합니다.
- httpWebRequest header에 앞서 설정한 토큰을 삽입하고 서버에 요청합니다.
- 서버에서 받은 response 데이터를 대본_번역 텍스트 파일에 저장하면 완성!  
