# React starter
[SAMPLE](https://stackblitz.com/edit/react-starter-sample)
## Create a react project
using create-react-app
```javascript=
create-react-app projectName
```

## Install dependencies

### REDUX
**Install**
```javascript=
npm install redux react-redux --save
```

**Setup**
```javascript=
import { Provider } from 'react-redux'
import { createStore } from 'redux'

const store = createStore(reducer)

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```


### redux-observable
**Install**
Also need install [rxjs](https://cn.rx.js.org/) and [redux](https://redux.js.org/)
```javascript=
npm install --save redux-observable
```

**Setup**
```javascript=
import { createStore, applyMiddleware } from 'redux'
import { createEpicMiddleware } from 'redux-observable'

import { rootEpic } from './modules/root'

const epicMiddleware = createEpicMiddleware()

const store = createStore(
  rootReducer,
  applyMiddleware(epicMiddleware)
)

epicMiddleware.run(rootEpic);
```


### redux-devtools-extension
**Install**
1. Google 應用商店下載插件
2. 透過 NPM 安裝`npm install  redux-devtools-extension --save-dev`

**Setup**
```javascript=
import { composeWithDevTools } from 'redux-devtools-extension'

const store = createStore(reducer, composeWithDevTools(
  applyMiddleware(...middleware),
  // other store enhancers if any
))
```


### redux-logger
**Install**
```javascript=
npm install redux-logger --save
```

**Setup**
```javascript=
import {createLogger} from 'redux-logger'

const loggerMiddleware = createLogger({collapsed: true})

const store = createStore(
  rootReducer,
  applyMiddleware(loggerMiddleware)
)
```

**preview**
![](https://i.imgur.com/JkHjva9.png)
