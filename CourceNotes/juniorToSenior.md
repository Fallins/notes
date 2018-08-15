# Udemy course NOTE

## SSH
### Create a connection
```=shell
# ssh user@host
ssh ben.liao@192.168.1.125
```


## Performance I
### Uglify JS, CSS...
透過刪除空白、最小化命名來壓縮檔案，來達到節省流量
[線上 Uglify 工具](https://skalman.github.io/UglifyJS-online/)
### Minimize Images
* 依照合適的用途來選擇檔案格式 :
小動畫: GIF
照片: JPEG
透明背景: PNG
ICON: SVG

* 按需加載 :
小螢幕時載入小圖
大螢幕時載入大圖

* 使用 CDN
* 移除圖片的 exif 資訊

[JPEG 線上壓縮工具](http://jpeg-optimizer.com/)
[PNG 線上壓縮工具](https://tinypng.com/)
[圖片 CDN 服務](https://www.imgix.com/)
[VIEW EXIF](https://www.verexif.com/en/)

### Critical Render Path
![](https://i.imgur.com/wfDUQLl.png)
* 盡可能最先載入 CSS，越快解析完，使用者的畫面越早呈現
* 盡可能在最後才載入 JS，因為會阻隔其他檔案的下載。

![](https://i.imgur.com/LVE2m07.png)
* script 標籤提供 async、defer 兩種屬性，可以用來避免中斷瀏覽器解析

![](https://i.imgur.com/rJBnYej.png)
* DOMContentLoaded: 觸發點是在HTML、CSS 載入完成，瀏覽器解析完之前
* Load: 觸發點是所有資源載入完畢、渲染完成之後

### Testing your page speed
[PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/)
[WebPageTest](https://www.webpagetest.org/)



## Performance II
### Code-Splitting
透過動態載入`import()` 僅載入當前頁面所需的 JS。

如果是使用 `create-react-app` 或 `next.js` ，則是已經設定好直接就可以使用 Code-Splitting 功能。

優點:
1. 減少初次載入時所需要下載的檔案大小，加快載入速度。
2. 減少頻寬浪費。假設使用者永遠沒進入到某頁面，則該頁面所需的 JS 則不會載入。

缺點:
1. 並不是一定會減少 `bundle.js` 的大小，因為對此 webpack 需要更多程式碼來處理這部分的規則，但理論上是會變小的。
2. 雖然切分之後的檔案通常很小，載入速度會較快，但在切換頁面時還是會有輕微閃爍。

綜合其優缺點，還是需要依照專案的需求來評估是否需要使用此功能，並不一定切割過後就會比較好。

[React 官方文檔](https://reactjs.org/docs/code-splitting.html)
[react-loadable(官方文檔上推薦的library)](https://github.com/jamiebuilds/react-loadable)
[Code-Splitting(by HOC)](https://github.com/aneagoie/code-splitting-exercise)

### React Performance Optimizations
所有父元件的 update 都會導致其子元件也 update。也就是說父元件的 props 或是 state 的改變都會造成子元件重新渲染，不管子元件是否真的需要重新渲染。

如何減少不必要的渲染以提升效能:
1. 利用 `shouldComponentUpdate(nextProps, nextState)` 來判斷該元件是否真的需要更新
2. 利用 React 提供的 Pure Component

但以上的方法都是藉由額外的判斷來決定是否更新，過度的濫用也有可能造成效能的浪費；
或是判斷沒寫好的話，有可能造成漏掉應該更新的時機，使用時須特別注意。

[Pure Component](https://juejin.im/entry/5934c9bc570c35005b556e1a)
[Why did you update](https://github.com/maicki/why-did-you-update)

### Progressive Web App(PWA)
由 [Google](https://developers.google.com/web/fundamentals/codelabs/your-first-pwapp/) 提供的解釋，什麼是 PWA:
 * 漸進增強 - 能夠讓每一位用戶使用，無論用戶使用什麽瀏覽器，因為它是始終以漸進增強為原則。
 * 響應式用戶界面 - 適應任何環境：桌面電腦，智能手機，筆記本電腦，或者其他設備。
 * 不依賴網絡連接 - 通過 service workers 可以在離線或者網速極差的環境下工作。
 * 類原生應用 - 有像原生應用般的交互和導航給用戶原生應用般的體驗，因為它是建立在 app shell model 上的。
 * 持續更新 - 受益於 service worker 的更新進程，應用能夠始終保持更新。
 * 安全 - 通過 HTTPS 來提供服務來防止網絡窺探，保證內容不被篡改。
 * 可發現 - 得益於 W3C manifests 元數據和 service worker 的登記，讓搜索引擎能夠找到 web 應用。
 * 再次訪問 - 通過消息推送等特性讓用戶再次訪問變得容易。
 * 可安裝 - 允許用戶保留對他們有用的應用在主屏幕上，不需要通過應用商店。
 * 可連接性 - 通過 URL 可以輕松分享應用，不用復雜的安裝即可運行。


透過 [Progressive Web App Checklist](https://developers.google.com/web/progressive-web-apps/checklist) 了解要成為最基礎的 PWA 需要具備的條件。

#### HTTPS
安全性是PWA的基礎條件之一，而透過 HTTPS 可以讓我們獲得相對安全的環境。
HTTPS 的主要思想就是，用戶相信憑證頒發機構所發出的憑證，因此用戶也相信取得此憑證的網站是合法且安全的。[[WIKI]](https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%AE%89%E5%85%A8%E5%8D%8F%E8%AE%AE)

提供免費認證的服務
[Let’s Encrypt](https://letsencrypt.org/)
[cloudflare](https://www.cloudflare.com/zh-tw/lp/overview-a/)

#### App Manifest
如果是透過 `create-react-app` 來產生專案的話，會自動在 `public/` 產生一個 `manifest.json` 檔案。

manifest 設定檔能夠幫我們設定像是自訂名稱、自訂圖標、設定啟動畫面、顯示方向和加到主畫面等功能。

並且可以在 Chrome Dev Tool 下面的 Application tab 下面看到相關的資訊。
![](https://i.imgur.com/DotExiy.png)

```jsonld=
// 透過 create-react-app 產生的最基本款
{
  "short_name": "React App",
  "name": "Create React App Sample",
  "icons": [
    {
      "src": "favicon.ico",
      "sizes": "64x64 32x32 24x24 16x16",
      "type": "image/x-icon"
    }
  ],
  "start_url": "./index.html",
  "display": "standalone",
  "theme_color": "#000000",
  "background_color": "#ffffff"
}

```

[PWA 相關文檔](https://lavas.baidu.com/pwa/engage-retain-users/add-to-home-screen/introduction)
[PWA 30天鐵人賽](https://ithelp.ithome.com.tw/articles/10187529)

#### Service Worker
Service Worker 提供了新的體驗，讓用戶可以在網路不佳甚至是斷線時，依舊可以擁有基礎的體驗(不至於像是一般的WEB斷線會有小恐龍出現)。

並且還可以做到像是更新或是推播這種原本應該是 APP 才能做到的功能。

一般來說，用戶在瀏覽網頁時都是向伺服器發出請求，再由伺服器回應資料(HTML、CSS、JS等等)。

而 SW(Service Worker 簡稱) 有點像是中間人的感覺，一旦你的應用程式註冊了 SW ，接下來發出的所有請求都會被其攔截，並拿去詢問 Cache API 。

如果已經有資料了，便直接回傳給用戶；若無則再向伺服器發起請求。

![](https://i.imgur.com/xx1yE2z.png)

在 Chrome Dev Tool 中一樣可以透過 Application 這個 tab 來查看。紅框部分則是 Cache 的部分，SW 會將需要快取的資料存放在此。

![](https://i.imgur.com/XiCoD5q.png)

如果是透過 `create-react-app` 那 SW 的部分則都設定完成了。如果需要自己設定可以參考[這裡](https://github.com/jeffposnick/create-react-pwa/compare/starting-point...pwa)

### Deploy React App on github pages
#### Install
```javascript=
npm install --save gh-pages
```

#### Usage
在 `package.json` 中加入新的 `scripts`，並加入 `homepage` property。
```javascript=
"homepage": "https://fallins.github.io/notes"
"scripts": {
    "predeploy": "npm run build"
    "deploy": "gh-pages -d build"
}

```


## Testing
 * Unit Tests
 * Integration Tests
 * Automation Tests
### Refference
[React 前端單元測試教學](https://medium.com/@savemuse/react-%E5%89%8D%E7%AB%AF%E6%B8%AC%E8%A9%A6%E6%95%99%E5%AD%B8-2ccedbe79411)
[自動軟體測試、TDD 與 BDD](https://medium.com/@yurenju/%E8%87%AA%E5%8B%95%E8%BB%9F%E9%AB%94%E6%B8%AC%E8%A9%A6-tdd-%E8%88%87-bdd-464519672ac5)


## SSR (Server Side Rendering)
### SSR VS CSR
CSR 需要在第一次時將所有需要用到的資源全部下載完後，使用者才能看到第一屏的畫面。
優點是後續的操作將會非常快，缺點則是初次訪問時必須下載較大量的資源。
![](https://i.imgur.com/3dC2Nkj.png)

SSR 則是取得HTML檔案後，透過解析的過程在去下載需要的 JS、CSS 檔案，使用者能先看到畫面。
但如果需要有完整的互動功能，與 CSR 一樣要等全部檔案下載解析完成後才能操作。
![](https://i.imgur.com/hRn3weS.png)

所以兩著之間最大的差別就是在於使用者看到首屏的時間。

**[Server-side vs Client-side Routing](https://medium.com/@wilbo/server-side-vs-client-side-routing-71d710e9227f)**
### Gatsby

### Next

#### Install
```javascript=
npm install --save next react react-dom
```

#### Setup
在跟目錄建立一個 `pages` 資料，並執行 start script。
`packages.json`
```javascript=
"scripts": {
    "start": "next"
}
```

#### Usage
在 `pages` 資料夾中新增兩個檔案，`index.js`、`about.js`。
Next 會使用資料夾中的檔案名來做 route，也就是說在新增了兩個檔案之後，我們可以直接訪問 `/index`、`/about` 這兩個頁面。

另外，Next 還提供了 Link 來提供給 Client 做頁面的切換，透過 Link 只會下載所需的檔案並不會重新向伺服器發起完整的請求。
如果是透過 a 標籤來做導向，則會發起完整的請求。

`index.js`
```javascript=
import Link from 'next/link'

const Index = () => (
    <div>
        <h1>this is index page.</h1>
        <Link href='/about'>
            <button>About</button>
        </Link>
        
        
        //<a href='/about'>About</a>   
        
    </div>
)

export default Index
```

`about.js`
```javascript=
import Link from 'next/link'

const About = () => (
    <div>
        <h1>this is about page.</h1>
        <Link href='/index'>
            <button>Back</button>
        </Link>
    </div>
)

export default About
```


#### Refference
**another choice for SEO**
[prerender.io](https://prerender.io/)

## Security
![](https://i.imgur.com/ilf9rzs.png)
### SQL Injection

### 3rd Party Libraries
#### nsp (Node Security Platform)
已於 2018/04 被 NPM [收購](https://medium.com/npm-inc/npm-acquires-lift-security-258e257ef639)，會繼續提供服務直到 2018/09 ，之後安全性檢查的功能將由 NPM 提供(NPM@6 之後)，[透過 `npm audit` 取代原本nsp的檢查](https://blog.npmjs.org/post/175511531085/the-node-security-platform-service-is-shutting)。

[nsp](https://github.com/nodesecurity/nsp) 會幫忙檢查所有使用到的套件是否有安全性的問題
##### Install & Usage
```javascript=
// Install
npm install nsp -g

// Usage
nsp check
```
檢查出有漏洞的套件，及其版本、路徑等等資訊。
![](https://i.imgur.com/FMsaqV9.png)
#### [snyk](https://github.com/snyk/snyk)
另一個可以檢查所有相依套件的漏洞的套件，但是與 nsp 一樣的共同問題就是套件之間的相依是層層嵌套的。
假設A套件底下的B套件在某個版本有安全性漏洞。雖然在下個版本修復了，但是A套件並沒有相對的更新，導致B套件更新之後A套件也不能用了，於是就只能等待A套件的更新，或是不使用A套件，目前沒有好的解法只能從中取捨。




### Logging
#### [morgan](https://github.com/expressjs/morgan)
使用簡單，幫助紀錄HTTP Request 的 LOG。

#### [winston](https://github.com/winstonjs/winston/tree/2.x)
全方位 Logger 工具(? ，可以客製化logger。


### HTTPS Everywhere
如上面提到的，透過 Https 來保護機敏性資料的傳送。

### XSS (Javascript Injection)
XSS 透過與使用者的互動來達到攻擊目的。最常見的就是留言版的頁面，如果攻擊者透過留言板輸入惡意的代碼，網站又沒有做好防護(例如: 未過濾使用者的輸入、輸出時候也沒有過濾HTML Tag等等)，就會導致其他使用者在進到此頁面時被攻擊竊取資訊。

[XSS攻擊的深入探討與防護之道](https://www.qa-knowhow.com/?p=2992)

### CSRF (Cross-Site Request Forgery)
[讓我們來談談 CSRF](https://blog.techbridge.cc/2017/02/25/csrf-introduction/)



### Reference
[2017鐵人賽資安系列](https://ithelp.ithome.com.tw/articles/10186125)