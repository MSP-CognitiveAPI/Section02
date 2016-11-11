# Section02
Cog.io Section02

##Cogio YoutubeScript project
Cogio 유튜브 스크립트 프로젝트는 자마린과 애저 코그니티브 서비스를 이용한 프로젝트입니다.



##Cogio YoutubeScript project Azure Cognitive 부분

###1. 초기 셋팅
[!초기화](https://github.com/cog-io/Section02/blob/master/picture/initialize.PNG)

- Azure Cognitive Speech api를 쓰기 위해서는 **DataRecognitionClient** 의 변수가 필요합니다.
 위의 화면에서는 m_dataClient라는 변수로 이를 이용합니다.
- speech api에서 화자의 음성을 인식하는 방법은 크게 2가지로 나뉩니다. 화자의 마이크 받은 데이터를 텍스트로 변 환하는 기술과 기존 음성파일에 있는 데이터를 텍스트로 바꾸는 기술을 들수 있습니다. YoutubeScript에서는 기존 음성파일의 데이터를 애저에 보내서 인식하는 과정을 거칩니다. **SpeechRecognitionMode** 에서 longDictation기능은 긴 음성 파일을 애저로 보내주는 매서드를 담당하고 있습니다.
- DefaultLocale은 애저서버로 음성파일을 보낼때 어떤 언어로 바꿀것인지 고르는 선택 배열입니다.
- primarykey는 애저서버에서 할당하는 accesstoken입니다.
- translate_SubscriptionKey는 애저서버에서 translator api를 쓸때 쓰는 토큰키입니다.
