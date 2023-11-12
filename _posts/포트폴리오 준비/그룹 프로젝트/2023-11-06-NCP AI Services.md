# Naver Cloud Platform에서 제공하는 AI Servies

네이버 부스트캠프 웹·모바일 8기 그룹 프로젝트 진행에 있어, 특정 한도 내의 NCP 크레딧을 사용할 수 있게 되었다.

이에 따라 서비스 기획 단계인 1주차에 CLOVA API를 포함한 각종 AI Services를 검토해 우리가 개발할 서비스에 NCP API를 활용할 방안을 고민해 보았다.

# AI Services 목록

## 목록

[NAVER CLOUD PLATFORM](https://www.ncloud.com/product/aiService)

<img width="1042" alt="%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-11-06_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11 13 06" src="https://user-images.githubusercontent.com/138586629/281240432-8801208d-c35e-4462-8424-fab9c405bb70.png">

<img width="1050" alt="%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-11-06_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_11 13 53" src="https://user-images.githubusercontent.com/138586629/281240444-75b33cbb-1c28-4bac-81c7-c8ff82961cd0.png">

## <별 하나에 글 하나>에 사용할 서비스 후보

- Papago Translation API
  [Papago Translation API (링크)](https://www.ncloud.com/product/aiService/papagoTranslation)
  - 의견 : 작성한 글을 다국어로 번역하여 글로벌 서비스를 지향할 수 있음
- CLOVA Sentiment
  [CLOVA Sentiment (링크)](https://www.ncloud.com/product/aiService/clovaSentiment)
  - 의견 : 작성한 글을 감정분석하여 분석 결과에 따라 다른 별 테마, 배경음악, Voice 옵션을 적용할 수 있음
- CLOVA Voice
  [CLOVA Voice (링크)](https://www.ncloud.com/product/aiService/clovaVoice)
  - 의견 : 작성한 글을 읽어주는 서비스를 만들 수 있음; 접근성(accessibility) 측면도 고려 가능
- CLOVA Speech Recognition (CSR)
  [CLOVA Speech Recognition (CSR) (링크)](https://www.ncloud.com/product/aiService/csr)
  - 의견 : 사용자가 본인의 목소리로 받아쓰기 하여 글을 작성할 수 있음; 접근성 측면도 고려 가능

# API 사용법

## Papago Translation API

> 네이버 Papago에 적용된 번역 REST API
> 입력된 텍스트를 다른 나라 언어(영어, 중국어)로 번역해 출력

[Papago Translation API 공식문서 (링크)](https://api.ncloud-docs.com/docs/ai-naver-papagonmt-translation)

```bash
curl -i -X POST \
   -H "X-NCP-APIGW-API-KEY-ID:{앱 등록 시 발급받은 Client ID}" \
   -H "X-NCP-APIGW-API-KEY:{앱 등록 시 발급 받은 Client Secret}" \
   -H "Content-Type:application/json" \
   -d \
'{
  "source": "{원본 언어 코드}",
  "target": "{번역 결과 언어 코드}",
  "text": "{번역할 text}"
}' \
 'https://naveropenapi.apigw.ntruss.com/nmt/v1/translation'
```

```js
// 네이버 Papago Text Translation API 예제
var express = require("express");
var app = express();
var client_id = "YOUR_CLIENT_ID";
var client_secret = "YOUR_CLIENT_SECRET";
var query = "번역할 문장을 입력하세요.";
app.get("/translate", function (req, res) {
  var api_url = "https://naveropenapi.apigw.ntruss.com/nmt/v1/translation";
  var request = require("request");
  var options = {
    url: api_url,
    form: { source: "ko", target: "en", text: query },
    headers: {
      "X-NCP-APIGW-API-KEY-ID": client_id,
      "X-NCP-APIGW-API-KEY": client_secret,
    },
  };
  request.post(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
      res.writeHead(200, { "Content-Type": "text/json;charset=utf-8" });
      res.end(body);
    } else {
      res.status(response.statusCode).end();
      console.log("error = " + response.statusCode);
    }
  });
});
app.listen(3000, function () {
  console.log("http://127.0.0.1:3000/translate app listening on port 3000!");
});
```

## CLOVA Sentiment

> 텍스트 데이터를 분석해서 해당 단어, 문장, 문구 내용의 감정을 분석하는 서비스로 그 결과를 반환하는 HTTP 기반의 REST API

[CLOVA Sentiment API 공식문서 (링크)](https://api.ncloud-docs.com/docs/ai-naver-clovasentiment-api)

```bash
curl -i -X POST \
   -H "X-NCP-APIGW-API-KEY-ID:{앱 등록 시 발급받은 Client ID}" \
   -H "X-NCP-APIGW-API-KEY:{앱 등록 시 발급 받은 Client Secret}" \
   -H "Content-Type:application/json" \
   -d \
'{
  "content": "{감정분석 Text}"
}' \
 'https://naveropenapi.apigw.ntruss.com/sentiment-analysis/v1/analyze'
```

## CLOVA Voice

> 음성으로 변환할 텍스트와 음색, 속도, 감정 등을 파라미터로 입력받은 후 음성을 합성하여 그 결과를 반환하는 HTTP 기반의 REST API

[CLOVA Voice API 공식문서 (링크)](https://api.ncloud-docs.com/docs/ai-naver-clovavoice-ttspremium)

```js
// 네이버 음성합성 Open API 예제
var express = require("express");
var app = express();
var client_id = "YOUR_CLIENT_ID";
var client_secret = "YOUR_CLIENT_SECRET";
var fs = require("fs");
app.get("/tts", function (req, res) {
  var api_url = "https://naveropenapi.apigw.ntruss.com/tts-premium/v1/tts";
  var request = require("request");
  var options = {
    url: api_url,
    form: {
      speaker: "nara",
      volume: "0",
      speed: "0",
      pitch: "0",
      text: "좋은 하루 되세요",
      format: "mp3",
    },
    headers: {
      "X-NCP-APIGW-API-KEY-ID": client_id,
      "X-NCP-APIGW-API-KEY": client_secret,
    },
  };
  var writeStream = fs.createWriteStream("./tts1.mp3");
  var _req = request.post(options).on("response", function (response) {
    console.log(response.statusCode); // 200
    console.log(response.headers["content-type"]);
  });
  _req.pipe(writeStream); // file로 출력
  _req.pipe(res); // 브라우저로 출력
});
app.listen(3000, function () {
  console.log("http://127.0.0.1:3000/tts app listening on port 3000!");
});
```

## CLOVA Speech Recognition (CSR)

> HTTP 기반의 REST API로 제공하는 음성인식 API
> 인식에 사용할 언어와 음성 데이터를 입력받고 그에 맞는 인식 결과를 텍스트로 반환

[CLOVA Speech Recognition (CSR) API 공식문서 (링크)](https://api.ncloud-docs.com/docs/ai-naver-clovaspeechrecognition-stt)

```js
const fs = require("fs");
const request = require("request");

const clientId = "YOUR_CLIENT_ID";
const clientSecret = "YOUR_CLIENT_SECRET";

// language => 언어 코드 ( Kor, Jpn, Eng, Chn )
function stt(language, filePath) {
  const url = `https://naveropenapi.apigw.ntruss.com/recog/v1/stt?lang=${language}`;
  const requestConfig = {
    url: url,
    method: "POST",
    headers: {
      "Content-Type": "application/octet-stream",
      "X-NCP-APIGW-API-KEY-ID": clientId,
      "X-NCP-APIGW-API-KEY": clientSecret,
    },
    body: fs.createReadStream(filePath),
  };

  request(requestConfig, (err, response, body) => {
    if (err) {
      console.log(err);
      return;
    }

    console.log(response.statusCode);
    console.log(body);
  });
}

stt("Kor", "음성 파일 경로 (ex: ./test.wav)");
```
