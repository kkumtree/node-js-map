# Node.js란 무엇일까? 


## MAP API를 사용하기 위한 기본적인 학습
### 가볍게 만들때 쓰는 것으로만 알고 있지, 한번도 직접 쳐보지도 세팅도 안해봤다...
- 참고: Node.js 교과서(저자: 조현영),  [**윤새연님 velog**](https://velog.io/@juneverbena/Javascript-웹에-지도-띄워보기-feat.-카카오-지도-API-1)


## 📅 자습기간
- 21.06.22. ~ 21.06.23.

## 🚀 Node.js 설치하기(Window)
- 기존 설명은 Mac 기반인데, 윈도우라고 딱히 다른 것이 없다. 
- 바이너리 설치는 아직도 헤메기 때문에, msi 인스톨러로 진행
- [**chocolatey**](https://steemit.com/kr/@orlein/chocolatey) 설치를 권장한다고 한다. 뭐지 이건.  
윈도우용 apt 패키지 매니저 같은 것 같다.   
파워쉘에서 이것저것 설치스크립트가 흐르는 데, 설치가 은근 걸린다.  
(그냥 자바나 할 껄 그랬나.)
    ```bash
    // 설치 후에 버전 확인으로 정상 설치 확인
    $ node -v
    $ npm -v
    ```

## 🗺️ 지도 API 선정(Naver/Daum)
- 원래는 Naver를 쓰려고 했다. 계정도 Naver를 주로 쓰니까
- 하지만, 티커 갯수에 제한이 달려있어서 기각. 나도 원하지 않는다. ([**참조**](https://velog.io/@holim0/카카오-맵과-네이버-맵-api-사용해보기))
- 그래서 다음지도 API를 사용하기로 하였다.
- 카카오DEV API 사용하기: https://developers.kakao.com/product/map 
- 다음지도 WEB API: https://apis.map.kakao.com/web/ 
- 샘플의 JS + HTML로 body 부분에 넣으면 빠르게 도입할 수 있다. ㅡ

## 💻 Express 웹서버 시작하기
- npm에서 서버 제작 시 불편함을 해소하고, 편의기능을 추가한 웹서버 프레임워크.  
    (http 모듈의 요청과 응답 객체에 추가 기능 부여 가능)
- 설치방법: Express-generator를 npm 전역 설치 (콘솔 명령어이기 때문이라고 함)
- 주의사항: 권한문제로 윈도우에서는 권한설정을 따로 해야하는 듯...  
([**정책설정1**](https://docs.microsoft.com/ko-kr/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.1), [**정책설정2**](https://extbrain.tistory.com/118), [**VSCode 관리자 실행 설정**](https://hianna.tistory.com/549))
    ```bash
    $ npm i -g express-generator

    // 새 프로젝트 생성
    // express [프로젝트명] --view=[템플릿엔진, default: pug]
    $ express myexpress --view=ejs

    // npm 모듈 설치 (대상 폴더: 프로젝트명)
    // 프로젝트 생성하면 어차피 방법을 초반에 '친절하게' 알려준다. 
    $ cd myexpress && npm i 

    // 서버 실행(둘 중에 하나만 선택)
    // Express 디버깅 https://expressjs.com/ko/guide/debugging.html
    $ npm run start
    $ SET DEBUG=myexpress:* npm start
    ```
- 서버가 실행되는 동안 http://localhost:3000/ 와 http://localhost:3000/users 확인
- pug와 ejs 엔진 차이: https://namunotebook.tistory.com/12 (솔직히 ejs가 맘에든다)

## 🌠 트러블슈팅 
- 근데 지도 API 끌어와서 적용했는데, 작동이 안됨; 뭐지? 뭐긴뭐겠어 RTFM  
    JS 기반으로 쓰기 때문에 APP KEY는 JavaScript용을 써야한다고 한다.  
    무엇보다 가이드를 꼭 봐야하는데, '준비하기'에서 사이트 도메인을 등록해야 한다.   

## 🐍 뱀다리
- EJS 템플릿 엔진 살짝 다루기 (참고: https://velopert.com/379)  
    타이틀을 수정하고 싶었는데, 이걸 여유롭게 하려면 JS객체에 접근해야했다.  
    처음에는 객체라는 개념도 잘 몰랐기 때문에, 오류코드를 보고 접근을 했다.  
    자바스크립트 객체를 받아올 곳이 routes/index.js 였다.  
    title 부분을 수정하는 것으로 맛보기 끝.  
    포트번호는 당연히, bin/www 에서 포트번호를 변경할 수 있다. 