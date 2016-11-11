# Section02
Cog.io Section02

##Cogio YoutubeScript project
Cogio 유튜브 스크립트 프로젝트는 YoutubeExtractor dll과 Azure Cognitive service를 이용한 프로젝트 입니다.

##YoutubeExtractor
 - Overview
 YoutubeExtractor는 .NET용 라이브러리이며, C#으로 작성되어 있고 유튜브에서 비디오를 다운로드 할 수 있고 오디오 트랙을 추출할 수 있습니다. (현재는 플래시 비디오에서만 오디오 추출이 가능합니다.)

##Azure Cognitive service

### Bing Speech API
 Bing speech API는 음성을 텍스트로 변환하고 다시 음성으로 변환하여 의도를 이해합니다.

 - 음성 인식
 파일의 오디오나 마이크 또는 기타 오디오 소스의 라이브 음성을 포함한 음성 오디오를 실시간으로 텍스트로 변환합니다. 또한 실시간 스트리밍이 가능하므로 오디오가 서버로 전송될 때 부분 인식 결과도 반환됩니다.

 - 음성 의도 인식
 음성 오디오를 작업을 유도하는 의도로 변환합니다. 음성 의도 인식은 언어 인식 인텔리전트 서비스 모델을 사용하여 응용 프로그램이 음성을 텍스트로 변환할 뿐만 아니라 말하는 사람의 의도를 손쉽게 파악하여 앱 내에서 “알람 설정”과 같은 작업을 만들 수 있도록 해줍니다.

 - 텍스트 음성 변환
 텍스트를 음성 오디오로 변환합니다. 응용 프로그램이 사용자에게 다시 “말”해야 할 경우 이 API가 앱에서 생성된 텍스트를 사용자에게 재생 가능한 오디오로 변환합니다.

###Translator speech API
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
