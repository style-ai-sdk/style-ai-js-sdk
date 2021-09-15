# STYLE.AI Javscript SDK

## 설치 예

[바로가기](#예시)


## SDK 설치 무조건 따라하기

### 설치 및 초기화

우리가 가장 먼저 해야 할 일은 SDK 설치와 초기화입니다. SDK는 javascript 파일로 이루어져 있습니다.  
javascript 파일을 다운로드 받아 초기화하기 위해서 HTML 문서의 `<head></head>`태그 맨 마지막 부분에다음 두줄을 추가합니다.

```html
<!-- 순서 중요! -->
<script src="//style-ai-sdk.github.io/style-ai-js-sdk/style-ai.js"></script>
<script>STYLEAI.init({ apiKey: "<apiKey>", productId: "<productId>" })</script>
```
위 코드에서 `<apiKey>`와 `<productId>` 부분이 보이시나요?  
이 부분에는 각자 인증을 위해서 발급받은 `apiKey`와 어떤 상품에 대한 추천을 받을지 결정하기 위한 상품번호, `productId`를 넣어주어야 합니다.
위 두가지 값이 준비 되었으면, 위에서 입력한 코드의 해당 부분에 채워넣습니다. 

만약 `apiKey`가 `akkkaskfkkk4k4kk32445kl23ljkll`이고, `productId`가 `12345678`이라고 할 때, 전체 `head` 의 내용은 다음과 유사해야합니다.

```html
<head>
  ...기존에 있던 다른 내용들...
  <script src="https://style-ai-sdk.github.io/style-ai-js-sdk/style-ai.js"></script>
  <script>STYLEAI.init({ apiKey: "akkkaskfkkk4k4kk32445kl23ljkll", productId: "12345678" })</script>
</head>
```
⚠️ `src`와 `apiKey`, `productId` 값 주변의 따옴표 `"..."`에 유의하시기 바랍니다.

여기까지 문제 없이 진행 했으면 [영역지정](#영역지정) 항목으로 넘어갑니다. 아직 화면에는 아무런 변화가 없는 것이 정상입니다.  
진행하는데 문제가 있으면 다음 문제해결 항목을 참조합니다.

#### 문제해결

- __`productId` 값은 어떻게 알 수 있나요? :__  
  이용하시는 쇼핑몰에 따라서 서로 다르기 때문에 한 가지의 방법으로 안내드리기는 어렵습니다. 해당 쇼핑몰의 가이드를 따르시기 바랍니다.   
  본사에서 지원하는 특정 쇼핑몰의 경우, `style-ai.js`가 아닌 다른 파일 주소로 안내 받으셨을 수 있습니다. 이런 경우, `productId` 값을 생략하시고 다음과 같이 간단하게 초기화 할 수
  있습니다.
  ```html
  <script src="https://style-ai-sdk.github.io/style-ai-js-sdk/<쇼핑몰별 제공파일>.js"></script>
  <script>STYLEAI.init({ apiKey: "<apiKey>" })</script>
  ```
- __`head` 태그 안에서는 `productId` 값을 넣을 수가 없어요 :__  
  사용하시는 쇼핑몰 프로그램에 따라서 특정 위치에서 `productId`값을 넣을 수 없을 수도 있습니다.   
  그런경우, 위 코드를 `productId`에 접근 가능한 특정 위치에 넣어도 상관 없습니다. 가령, `body` 태그의 맨 마지막에 넣어도 문제 없습니다.

### 영역지정

영역지정은 추천상품을 화면 어디에 보여줄 지 정하는 단계입니다.  
아래 단계를 진행하고 나면 원하는 영역에 상품 추천이 나타나게 됩니다.

#### 기본 렌더방식

HTML `body`내에 상품 추천을 노출하고 싶은 부분에 다음과 같이 입력합니다.

```html
<div data-style-ai-render="recommend"></div>
```

#### 버튼을 이용한 오버레이 방식

상품 추천 모달 팝업을 띄우고 싶으면 팝업 생성 버튼으로 사용하고 싶은 요소에 다음과 같이 입력합니다.

```html
<button data-style-ai-open-layer="recommend">상품 추천 보기 (버튼 문구 자유입력)</button>
```

##### 버튼 스타일 변경

모달 팝업을 띄우기 위한 버튼의 태그이름과 내용은 아무 요소나 원하는 대로 지정할 수 있습니다.   
또한 지정된 속성 외에 다른 속성을 자유롭게 추가해도 상관 없으므로
`class`, `style` 속성등을 추가하여 CSS로 자유롭게 스타일을 변경할 수 있습니다.

```html
<div data-style-ai-open-layer="recommend" class="recommend-popup">
  <span class="icon"/>추천 제품 더 보기
</div>
```

## 반응형 디자인

기본 템플릿 UI는 반응형 디자인으로 해당 영역의 width가 1000px이하이면 태블릿, 550px 이하이면 모바일 기기용 레이아웃을 렌더링합니다. PC 모드에서는 한 화면에 최개 3개, 태블릿에서는 2개,
모바일에서는 1개의 추천이 보여지며, 이보다 많은 추천 스타일이 존재할 경우 좌우로 슬라이드 가능한 Carousel 형태로 나타납니다.

반응형 스타일의 기준 width는 다음과 같이 HTML에 지정한 영역 태그에 속성을 추가하여 변경할 수 있습니다. 값의 순서는 상관 없으며, 둘 중 큰 값이 태블릿 기준, 작은 값이 모바일 기준이 됩니다.

```html
<!-- 기본렌더방식, 1200이하 태블릿, 700 이하 모바일 -->
<div data-style-ai-render="recommend" data-style-ai-device-sizes="700,1200"></div>

<!-- 오버레이방식, 900이하 태블릿, 400 이하 모바일 -->
<div data-style-ai-open-layer="recommend" data-style-ai-device-sizes="900,400"></div>
```

좀더 다양하게 디자인을 커스텀 하고 싶다면, [사용자 템플릿 사용](#사용자-템플릿-사용) 항목을 참조하기시 바랍니다.

## 고급 기능

자바스크립트를 다룰 수 있는 사용자들이 더욱 다양한 기능을 활용할 수 있도록 고급 기능을 제공합니다.

### 상세설정

위 간단 설치에서 입력한 초기화 코드중 `STYLEAI.init` 함수에 다음과 같이 추가로 상세 옵션을 설정할 수 있습니다. 특히 `externalLogData` 항목을 활용하면 이용 로그에 기록할 데이터를 추가로
지정할 수 있습니다.

```html
<head>
  ...
  <script src="https://style-ai-sdk.github.io/style-ai-js-sdk/style-ai.js"></script>
  <script>
    STYLEAI.init({
      apiUrl: '{호출할 API URL}',
      apiKey: '{사이트별로 발급된 API Key}',
      productId: '{현재 상품 ID}',
      displayBrandName: true, // brand명 표시 여부 (기본값 false)
      externalLogData: {
        // 로그에 기록하고 싶은 추가 데이터 (자유형식)
        age: '10-20',
        shopName: '나의 쇼핑몰'
      }
    })
  </script>
</head>
```

### 상품아이디 변경

Single Page App 등의 환경에서 화면의 새로고침 없이 상품번호나 다른 설정이 변경되는 경우, 다음과 같이 동적으로 변경해줄 수 있습니다.

```js
STYLEAI.render({ 
  productId: '{현재 상품 ID}',
  displayBrandName: true, // optional, init시의 설정을 덮어쓴다. 
})
```

상품 아이디 자동인식을 제공하는 쇼핑몰의 경우 다음과 같이 간단히 호출하면 실행 시점에 자동으로 현재 상품명을 인식하여 업데이트 합니다.

```js
STYLEAI.render()
```

### 슬라이드 컨트롤

좌우로 슬라이드 가능한 Carousel 형태일 경우, 슬라이드를 수동으로 컨트롤 할 수 있습니다.  
다음과 같이 추천 스타일을 렌더링할때 지정했던 HTML요소를 `STYLEAI.of` 함수에 넘겨주면 슬라이드를 수동으로 컨트롤 할 수 있습니다.

HTML

```html
<div data-style-ai-render="recommend" id="my_recommends1"></div>
```

javascript

```javascript
const $element = document.getElementById('my_recommends1');

STYLEAI.of($element).next() // 다음
STYLEAI.of($element).prev() // 이전
STYLEAI.of($element).goto(0) // 0,1,2
```

### 사용자 템플릿 사용

다른 마크업이나 디자인을 적용하고 싶을 때 다음과 같이 사용자가 직접 작성한 마크업을 적용할 수 있습니다.  
먼저 템플릿이 될 `script` tag를 작성합니다. 아래에서 참조하기 위해 id값을 지정해줍니다. 여기서는 `my-render-template-1`로 하겠습니다.

```html
<script type='template' id="my-render-template-1">
  <div class="custom-template-container">
    <% recommends.forEach(function(recommend){ %>
      <div>
        <div><%= recommend.styleName %></div>
        <img src="<%= recommend.styleOutImageUrl %>" alt="">
  
        <ul>
          <% recommend.recommendItems.forEach(function(recommendItem){ %>
          <li>
            <a href="<%= recommendItem.detailUrl %>" target="_blank">
              <img src="<%= recommendItem.imageUrl %>" alt="">
              <div><%= recommendItem.name %></div>
              <div><%= recommendItem.price %>원</div>
            </a>
          </li>
          <% }) %>
        </ul>
      </div>
    <% }) %>
  </div>
</script>
```

렌더링 영역에 `data-style-ai-template` 속성을 추가하여 해당 위치에 렌더링할 템플릿의 id를 지정해줍니다.

```html
<div data-style-ai-render="recommend" data-style-ai-template="my-render-template-1"></div>
```

오버레이 형식에도 동일하게 적용할 수 있습니다. 이때는 모달팝업 내부에 지정한 템플릿이 렌더링됩니다.

```html
<button data-style-ai-open-layer="recommend" data-style-ai-template="my-render-template-1">추천상품 보기</button>
```

템플릿 문법은 `jQuery`나 `lodash`의 [template](https://lodash.com/docs/4.17.15#template) 문법과 동일하며, 전달되는 데이터의 형식은 아래와 같습니다.

```js
{
  recommends :[
    {
      "styleName": String,
      "styleNo": Number,
      "styleOutImageUrl": String,
      "originalItem": {
        "recommendId": String,
        "itemId": String,
        "name": String,
        "productId": String,
        "price": Number,
        "originalPrice": Number,
        "imageUrl": String,
        "detailUrl": String,
        "brand": String
      },
      "recommendItems": [
        {
          "recommendId": String,
          "itemId": String,
          "name": String,
          "productId": String,
          "price": Number,
          "originalPrice": Number,
          "imageUrl": String,
          "detailUrl": String,
          "brand": String
        },
        {...}, 
        {...},
        //...
      ]
    },
    {...},      
    {...},
    //...
  ]
}
```

### 문제해결

__React를 이용해서 구성된 SPA사이트에 SDK를 추가하려 합니다. url parameter가 바뀔때 마다 `STYLEAI.render` 함수를 실행해서
`productId`를 업데이트 하려는데요, 화면상에 아무것도 나오지 않습니다. 어떻게 해야 할까요? :__  
  
STYLEAI.render를 실행하는 시점에 `data-style-ai-render="recommend"`나 `data-style-ai-open-layer="recommend"`가 지정되어 있는 DOM요소가
화면에 렌더링 되어 있어야 합니다. 보통 url이 변경된 후에 data를 fetch하고 나서 화면을 그리기 때문에, `STYLEAI.render`를 실행하는 시점이
화면이 그려지기 이전이 아닌지 검토해보아야 합니다.

아래는 일반적인 React 컴포넌트에서 흔히 발생할 수 있는 case입니다.

```jsx
const API_KEY = "...";

const MyComponent = () => {
  const { params:{ productId }} = useRouteMatch()
  const [ product, setProduct ] = useState();
  
  useEffect(() => {
    // 1. 여기에서 실행하면 실패합니다.
    // STYLEAI.init({ apiKey: API_KEY, productId })
    
    API.fetchProduct({productId}).then(({data}) => {
      setProduct(data);
      // 2. 여기에서 실행해도 실패합니다.
      // STYLEAI.init({ apiKey: API_KEY, productId })
    })
    // 3. 여기도 마찬가지입니다.
    // STYLEAI.init({ apiKey: API_KEY, productId })
  }, [productId])
  
  useEffect(() => {
    if(product){
      // 4. 여기에서 실행하는 것이 가장 안전합니다.
      STYLEAI.init({ apiKey: API_KEY, productId })
    }
  }, [product])

  return (
    <div>
      {product 
        ? <>
          <Products data={product} />
          <div data-style-ai-render="recommend" />
        </>
        : <Loading />
      }      
    </div>
  );
}
```

위 예시의 경우 1, 2, 3 번 위치에서 초기화를 시도할 시 `product` state가 아직 세팅되기 전이기 때문에
`<div data-style-ai-render="recommend" />` 엘리먼트가 아직 화면에 존재하기 않아 초기화가 실패하게 됩니다.

4번 과 같이 product가 로딩되고, 이에 따라서 필요한 element가 렌더링 된 것을 확신하는 시점에서 초기화를 실행해야만
SDK를 올바르게 초기화 할 수 있습니다.

## 예시

이 문서에서 설명한 설치방법을 적용해둔 HTML문서입니다. 아래 문서를 열고 소스보기를 하면 어떻게 구성되어있는지 알 수 있습니다.
- [종합예시](./example/style-ai.html)
  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
<br/>  
&nbsp;

