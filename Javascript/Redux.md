# Redux

## Install
```javascript=
npm install react-redux --save
```

## Setup
* Provider   : 將 store 傳遞給所有子組件
* createStore: 傳入 reducer 以創建 store

```javascript=
import { Provider } from 'react-redux'
import { createStore } from 'redux'
import rootReducer from './reducers'

const store = createStore(rootReducer)

ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>,
    document.getElementById('root')
)
```

* combineReducers
如果有多個 reducer 時，要先將他們結合。
每個 reducer 的命名以及嵌套關係都會影響最終 store 的結構，也可以多次combine 組合出需要的結構。
```javascript=
import { combineReducers } from 'redux'

// A reducer
export const searchRobots = (state = initStateSearch, action) => {
	switch(action.type) {
		case CHANGE_SEARCH_FIELD: 
			return Object.assign({}, state, {searchField: action.payload})
		default:
			return state
	}
}

// B reducer
export const requestRobots = (state = initState, action) => {
	switch(action.type) {
		case REQUEST_ROBOTS_PENDING: 
			return Object.assign({}, state, {isPending: true})
		case REQUEST_ROBOTS_SUCCESS: 
			return Object.assign({}, state, {robots: action.payload, isPending: false})
		case REQUEST_ROBOTS_FAILED: 
			return Object.assign({}, state, {error: action.payload, isPending: false})
		default:
			return state
	}
}

export const rootReducer = combineReducers({
    searchRobots,
    requestRobots
})

// final structure to the store
{
    searchRobots: {...},
    requestRobots: {...}
}
```

## MiddleWare
![](https://i.imgur.com/nBkNQZR.png)
MiddleWare 會在 action 進入 reducer 之前攔截，等於是提供一個時機點去做一些處理。
```javascript=
import { Provider } from 'react-redux'
import { createStore, applyMiddleware } from 'redux'
import { createLogger } from 'redux-logger'
import rootReducer from './reducers'

const logger = createLogger()
const store = createStore(rootReducer, applyMiddleware(logger))

ReactDOM.render(
    <Provider store={store}>
        <App />
    </Provider>,
    document.getElementById('root')
)
```


## Usage
![](https://i.imgur.com/EoHdNRU.png)

### Action Types
將所有 action 的 type 設為一個常數，提高複用性以及減少錯字機會。

`actionTypes.js`
```javascript=
export const CHANGE_SEARCH_FIELD = "CHANGE_SEARCH_FIELD"
export const FETCH_A_DATA = "FETCH_A_DATA"
export const FETCH_B_DATA = "FETCH_B_DATA"
```

### Action & Action Creator
Action Creator 實際上就是一個回傳一個物件(也就是 Action)的 pure function。
Action 可以沒有 payload 但是一定要有 type 這個屬性。
`actions.js`
```javascript=
import { CHANGE_SEARCH_FIELD } from './actionTypes'

export const setSearchField = text => ({
	type: CHANGE_SEARCH_FIELD,
	payload: text
})
```

### Reducer
所有的 action 最後都會進入 reducer 中處理，用以修改 store 中的值。
Reducer 也必須是個 pure function。

`reducers.js`
```javascript=
import { CHANGE_SEARCH_FIELD } from './actionTypes'

const initState = {
	searchField: ''
}

export const searchRobots = (state = initState, action) => {
	switch(action.type) {
		case CHANGE_SEARCH_FIELD: 
			return Object.assign({}, state, {searchField: action.payload})
		default:
			return state
	}
}
```

### connect
connect 是由 `react-redux` 提供的一個 HOC(higher order component)

`connect([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])`
最常用的是 `mapStateToProps`、`mapDispatchToProps` ，兩個都是回傳一個物件。

`mapStateToProps` 是將此 component 需要的資料從 store 提取後，可直接或經過再處理後當成 props 傳給元件使用。

`mapDispatchToProps` 是將元件需要用到的 action 包裝過後提供給元件使用，一樣是透過 props 方式傳給元件

`App.js`
```javascript=
import React, { Component } from 'react';
import { connect } from 'react-redux'
import { setSearchField } from '../actions'
import CardList from '../components/CardList';
import SearchBox from '../components/SearchBox';
import Scroll from '../components/Scroll';
import './App.css';

const mapStateToProps = state => {
  console.log(state)
  return {
    searchField: state.searchField
  }
}

const mapDispatchToProps = dispatch => {
  return {
    onSearchChange: (e) => {
      dispatch(setSearchField(e.target.value))
    }
  }
}

class App extends Component {
  constructor() {
    super()
    this.state = {
      robots: []
    }
  }

  componentDidMount() {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(response=> response.json())
      .then(users => {this.setState({ robots: users})});
  }

  render() {
    const { robots } = this.state;
    const { searchField, onSearchChange } = this.props
    const filteredRobots = robots.filter(robot =>{
      return robot.name.toLowerCase().includes(searchField.toLowerCase());
    })
    return !robots.length ?
      <h1>Loading</h1> :
      (
        <div className='tc'>
          <h1 className='f1'>RoboFriends</h1>
          <SearchBox searchChange={onSearchChange}/>
          <Scroll>
            <CardList robots={filteredRobots} />
          </Scroll>
        </div>
      );
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(App);
```

## Async Actions

### redux-thunk
#### Install
`npm install --save redux-thunk`

#### Setup
透過 `applyMiddleware` 來使用`redux-thunk`，傳入`applyMiddleware`的順序代表 action 傳入 middleware 的順序

```javascript=
import thunkMiddleware from 'redux-thunk'

const store = createStore(
    rootReducer, 
    applyMiddleware(thunkMiddleware, logger)
)
```

#### Usage
##### Action types
三種類型: Pending、Success、Failed
`actionTypes.js`
```javascript=
export const REQUEST_ROBOTS_PENDING = "REQUEST_ROBOTS_PENDING"
export const REQUEST_ROBOTS_SUCCESS = "REQUEST_ROBOTS_SUCCESS"
export const REQUEST_ROBOTS_FAILED = "REQUEST_ROBOTS_FAILED"
```

##### Actions
`actions.js`
```javascript=
import { 	 
	REQUEST_ROBOTS_PENDING, 
	REQUEST_ROBOTS_SUCCESS, 
	REQUEST_ROBOTS_FAILED 
} from './actionTypes'

export const requestRobots = () => (dispatch) => {
	dispatch({ type: REQUEST_ROBOTS_PENDING })
	fetch('https://jsonplaceholder.typicode.com/users')
      	.then(response => response.json())
      	.then(data => dispatch({
      		type: REQUEST_ROBOTS_SUCCESS,
      		payload: data
      	}))
      	.catch(err => dispatch({
      		type: REQUEST_ROBOTS_FAILED,
      		payload: err.message
      	}))
}
```

##### Reducers
`reducers.js`
```javascript=
import { 
	REQUEST_ROBOTS_PENDING, 
	REQUEST_ROBOTS_SUCCESS, 
	REQUEST_ROBOTS_FAILED 
} from './actionTypes'

const initState = {
	isPending: false,
	robots: [],
	error: ''
}

export const requestRobots = (state = initState, action) => {
	switch(action.type) {
		case REQUEST_ROBOTS_PENDING: 
			return Object.assign({}, state, {isPending: true})
		case REQUEST_ROBOTS_SUCCESS: 
			return Object.assign({}, state, {robots: action.payload, isPending: false})
		case REQUEST_ROBOTS_FAILED: 
			return Object.assign({}, state, {error: action.payload, isPending: false})
		default:
			return state
	}
}
```

##### mapStateToProps、mapDispatchToProps
```javascript=
const mapStateToProps = state => {
  console.log(state)
  return {
    searchField: state.searchRobots.searchField,
    robots: state.requestRobots.robots,
    isPending: state.requestRobots.isPending,
    error: state.requestRobots.error
  }
}

const mapDispatchToProps = dispatch => {
  return {
    onSearchChange: (e) => {
      dispatch(setSearchField(e.target.value))
    },
    onRequestRobots: () => dispatch(requestRobots())
  }
}
```