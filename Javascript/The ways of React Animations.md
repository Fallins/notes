# The ways of React Animations

## CSS/JS
使用 CSS3 transiton 或 JS add/remove classes、setTimeout 等方法來產生動畫效果。

適用不需配合生命週期或簡單的漸變動畫（active、focus....)
```javascript=
<div 
    className={`type-categories inplay col-4 ta-c pd-t-10 ${leftSliderActiveTab == 0?'active':''}`}
    onClick={() => {
        setActiveTab(0)
    }}>

    <svg className={`icon mg-r-5 va w-25 h-25 ${leftSliderActiveTab == 0?'t-white':'t-dkgray-2'}`}>
        <use xlinkHref="#icon-ico_slider_inplay"></use>
    </svg>
    <div className="mg-t-3">
        {l.inplay}
    </div>
</div>
```


## ReactCSSTransitionGroup([ref](https://reactjs.org/docs/animation.html))
ReactTransitionGroup（提供 lifecycle hooks) 的封裝。
需提供必要參數(transitionProps)以及配合的CSS classes，有 Appear、Enter、Leave 等幾種狀態。

* **Appear**
預設為false，會在 ReactCSSTransitionGroup 首次掛載時觸發。（需要一開始就有內容才看得出效果）
* **Enter**
ReactCSSTransitionGroup 中內容改變時觸發
* **Leave**
ReactCSSTransitionGroup 中內容減少或無內容時觸發

[Official Sample](https://stackblitz.com/edit/react-mmiuuu)
---

> HOC
```javascript=
import React, {Component} from 'react'
import {connect} from 'react-redux'
import ReactCSSTransitionGroup from 'react-addons-css-transition-group'

export default (Comp, getDisplayFlag) => {
	class AnimationWrapper extends Component{
		render(){
			const {display} = this.props
			const transitionProps = {
				transitionName: "slideMenu",
				transitionEnterTimeout: 500,
				transitionLeaveTimeout: 300
			}

			return (
			    <ReactCSSTransitionGroup {...transitionProps}>
		                {display? <Comp {...this.props}/> : null}
		            </ReactCSSTransitionGroup>
			)
		}
	}

	const mapS2P = (state) => {
		//const {displayLeftSlider} = state

		return {display: getDisplayFlag(state)}
	}

	return connect(mapS2P)(AnimationWrapper)
}
```

> CSS
```css=
.slideMenu-enter {
  transform: translateY(-70%);
  
}

.slideMenu-enter.slideMenu-enter-active {
  transform: translateY(0);
  transition: all 500ms ease-in;
}

.slideMenu-leave {
  opacity: 1;
}

.slideMenu-leave.slideMenu-leave-active {
  opacity: 0.01;
  transition: opacity 300ms ease-in;
}
```
> Using
```javascript
const sliderWithAnimation = animationWrapper(Compo, state => state.displayLeftSlider)
```

## ReactMotion([ref](https://github.com/chenglou/react-motion/tree/master))
[Demo](https://stackblitz.com/edit/react-mmiuuu)


##	Demos
[tab Switch](http://jsbin.com/fevavafixe/1/edit?css,js,output)
[More Odds](http://jsbin.com/faxidicebi/edit?css,js,output)
[Choose Odds](http://jsbin.com/taxoge/edit?css,js,output)

