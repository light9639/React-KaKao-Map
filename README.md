# **:zap: React-Weather 템플릿**
**:sparkles: <a href="https://light9639.github.io/React-Weather/">React-Weather 템플릿</a> :sparkles:**
## **:tada: 카카오 개발자 사이트에서 계정 정보 생성하기**
![다운로드 (1)](https://user-images.githubusercontent.com/95972251/191654315-35e73a4d-9208-449d-8b1f-10af6d04868f.png)

:pushpin: 우선 <a href="https://developers.kakao.com/">카카오 개발자 사이트</a>에 접속하여 계정을 만들고 로그인 합니다.

:one: 메인 화면의 상단 메뉴 중 "내 애플리케이션"을 선택합니다.<br />

:two: 내 애플리케이션에서 "애플리케이션 추가하기"를 선택합니다.<br />

:three: 앱 아이콘, 앱 이름, 사업자명을 입력하고 저장합니다.<br />

:four: 저장이 완료되면 요약 정보 페이지에 생성된 "앱 키"가 보입니다.<br />

:five: 플랫폼 메뉴의 "Web플랫폼 등록"을 선택합니다.<br />

:six: 사이트 도메인을 입력한 후 저장합니다.<br />

:seven: Web 사이트 도메인이 등록된 것을 볼 수 있습니다.<br />

:eight: 여기서 삭제나 수정등을 하실 수 있습니다.<br />

## **:confetti_ball: 리액트 프로젝트 수정사항들**
- 우선 리액트 프로젝트를 생성합니다.

```bash
npx create-react-app kakaomap
```

- index.html의 head에 다음 내용을 추가합니다.

```bash
<meta http-equiv="Content-Security-Policy" content="default-src 'self' 'unsafe-inline' https://dapi.kakao.com http://*.daumcdn.net; script-src 'self' 'unsafe-inline' https://dapi.kakao.com http://*.daumcdn.net; img-src 'self' 'unsafe-inline' https://dapi.kakao.com http://*.daumcdn.net;">
<meta http-equiv="X-Content-Security-Policy" content="default-src 'self' 'unsafe-inline' https://dapi.kakao.com http://*.daumcdn.net; script-src 'self' 'unsafe-inline' https://dapi.kakao.com http://*.daumcdn.net; img-src 'self' 'unsafe-inline' https://dapi.kakao.com http://*.daumcdn.net;">

<script type="text/javascript" src="https://dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=발급받은키"></script>
```
- App.js를 다음과 같이 수정합니다.

```bash

import './App.css';
import { useEffect } from 'react';

function App() {

  //스크립트 파일 읽어오기
  const new_script = src => {
    return new Promise((resolve, reject) => {
      const script = document.createElement('script');
      script.src = src;
      script.addEventListener('load', () => {
        resolve();
      });
      script.addEventListener('error', e => {
        reject(e);
      });
      document.head.appendChild(script);
    });
  };

  useEffect(() => {
    //카카오맵 스크립트 읽어오기
    const my_script = new_script('https://dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=발급받은키');

    //스크립트 읽기 완료 후 카카오맵 설정
    my_script.then(() => {
      console.log('script loaded!!!');
      const kakao = window['kakao'];
      kakao.maps.load(() => {
        const mapContainer = document.getElementById('map');
        const options = {
          center: new kakao.maps.LatLng(37.56000302825312, 126.97540593203321), //좌표설정
          level: 3
        };
        const map = new kakao.maps.Map(mapContainer, options); //맵생성
        //마커설정
        const markerPosition = new kakao.maps.LatLng(37.56000302825312, 126.97540593203321);
        const marker = new kakao.maps.Marker({
          position: markerPosition
        });
        marker.setMap(map);
      });
    });
  }, []);

  return (
    <div className="App">
      <div id="map" className="map"/>
    </div>
  );
}

export default App;
```

- App.css에 class를 추가합니다.

```bash
.map {
  width: 100%;
  height: 600px;
  align-items: center;
  justify-content: center;
  margin-left: auto;
  margin-right: auto;
  border-style: solid;
  border-width: medium;
  border-color: #D8D8D8;
}
```
## **:dart: 완성화면**
![다운로드](https://user-images.githubusercontent.com/95972251/191654356-84a8ece3-eef9-48c5-96b0-607b8f80da7b.png)

- 지도의 좌표는 <a href="https://tablog.neocities.org/keywordposition.html">URL</a>에서 찾으시면 됩니다.

## **:paperclip: 출처**
- 출처1 : https://codegear.tistory.com/13
- 출처2 : https://codegear.tistory.com/14
