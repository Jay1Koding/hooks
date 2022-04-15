# hooks

https://codesandbox.io/s/nooks-wp8m57?file=/src/App.js

# useState

```javascript
import React, { useState } from 'react';

const App = () => {
  const [item, setItem] = useState(0);
  const increaseItem = () => {
    setItem(item + 1);
  };
  const decreaseItem = () => {
    setItem(item - 1);
  };
  return (
    <div className='App'>
      <h1>Hello {item}</h1>
      <button onClick={increaseItem}>+1</button>
      <button onClick={decreaseItem}>-1</button>
    </div>
  );
};
// class part
class AppUgly extends React.Component {
  state = {
    item: 1,
  };
  render() {
    const { item } = this.state;
    return (
      <div className='App'>
        <h1>Hello {item}</h1>
        <button onClick={this.increaseItem}>+1</button>
        <button onClick={this.decreaseItem}>-1</button>
      </div>
    );
  }
  increaseItem = () => {
    this.setState((state) => {
      return {
        item: state.item + 1,
      };
    });
  };
  decreaseItem = () => {
    this.setState((state) => {
      return {
        item: state.item - 1,
      };
    });
  };
}

export default AppUgly;
```

## useInput

- input 역할

```javascript
import React, { useState } from 'react';

const useInput = (initialValue, validator) => {
  const [value, setValue] = useState(initialValue);
  const onChange = (event) => {
    const {
      target: { value },
    } = event;
    let willUpdate = true;
    if (typeof validator === 'function') {
      willUpdate = validator(value);
    }
    if (willUpdate) {
      setValue(value);
    }
  };
  return { value, onChange };
};

const App = () => {
  const maxLength = (value) => !value.includes('@');
  const name = useInput('Mr.', maxLength);
  return (
    <div className='App'>
      <h1>Hello</h1>
      {/* <input placeholder="username" value={name.value} /> */}
      <input placeholder='username' {...name} />
    </div>
  );
};

export default App;
```

## useTabs

- 웹사이트에 메뉴 또는 무엇이든 간에 tab을 사용하기 쉽게 만들어줌

```javascript
import React, { useState } from 'react';

const contents = [
  {
    tab: 'Sec 1',
    content: 'im the content of Sec 1',
  },
  {
    tab: 'Sec 2',
    content: 'im the content of Sec 2',
  },
];

const useTabs = (initialTab, allTabs) => {
  const [currentIndex, setCurrentIndex] = useState(initialTab);
  if (!allTabs || !Array.isArray(allTabs)) {
    return;
  }
  return {
    currentItem: allTabs[currentIndex],
    changeItem: setCurrentIndex,
  };
};

const App = () => {
  const { currentItem, changeItem } = useTabs(0, contents);
  return (
    <div className='App'>
      <h1>Hello</h1>
      {contents.map((section, index) => (
        <button onClick={() => changeItem(index)}>{section.tab}</button>
      ))}
      <div>{currentItem.content}</div>
    </div>
  );
};

export default App;
```

---

# useEffect

## useTitle

- react document의 title을 몇 개의 hooks와 함께 바꿈

## usePageLeave

- 유저가 page를 벗어나는 시점을 발견하고 함수를 실행

## useClick

- element를 클릭하는 시점을 발견

## useFadeIn

- 어떤 element든 상관없이 애니메이션을 element 안으로 서서히 사라지게 만듬

## useFullscreen

- 어떤 element든 풀스크린으로 만들거나 일반 화면으로 돌아갈 수 있게 함

## useHover

- 마우스를 올렸을 때 감지

## useNetwork

- online인 지 offline 인 지 감지

## useNotification

- notification API를 사용할 때 유저에게 알림을 보내줌

## useScroll

- 스크롤을 사용할 때를 감지해 알려줌

## usePreventLeave

- 유저가 변경사항이나 무엇이든 간에 저장하지 않고 페이지를 벗어나길 원할 때 확인

## useConfirm

- ...

## useAxios

- HTTP requests client axios를 위한 wrapper
