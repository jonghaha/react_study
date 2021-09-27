# Study react.js

## 01.Virtual DOM
---
* react는 가상의 DOM인 Virtual DOM 제어하여 개발의 편의성과 성능 개선.

    * 렌더링 - JSX 문법을 사용한 ReactDOM.render()를 호출하면 생성.   
        index.js
        ```
        ReactDOM.render(<App />,document.getElementById('root'));
        ```
        index.html
        ```
        <div id="root"></div>
        ```
    index.html div 태그아아디 root 사이에 Virtual DOM 생성. -> ID는 원하는 걸로 변경 가능.


## 02.JSX
---
* Javascript를 확장한 문법이고 JS와 마크업으로 component 생성
```
function Hello() {
    return <h1>Hello</h1>;
}

function App() {
    return (
        <div>
            <Hello />
        </div>
    );
}
```
* 중괄호를 사용하여 attribute에 Javascript 삽입
```
const element = <img src={images.image} />
```
   
## 03.Component와 Props
* 함수 component와 클래스 component

함수 component
```
function App() {
    return <h1>Hello</h1>;
}
```
클래스 component
```
class App extends React.Component {
    render() {
        return <h1>Hello</h1>;
    }
}
```

* component에 props를 통하여 정보를 보낼 수 있음.
```
function Hello(props) {
    return <h1>Hello {porps.name}</h1>;
}
/*
function Hello({ name }}) {
    return <h1>Hello {name}</h1>;
}
*/

function App() {
    return (
        <div>
            <Hello name="lewis" />
        </div>
    );
}
```

* Dynamic Component
```
function Hello({ name }}) {
    return <h1>Hello {name}</h1>;
}

const studyName = [
    {
        name: "insik"
    },
    {
        name: "jack"
    },
    {
        name: "julia"
    },
    {
        name: "june"
    },
    {
        name: "lewis"
    },
    {
        name: "evelyn"
    }
]

function App() {
    return (
        <div>
            {studyName.map(names => (
                <Hello name={names.name} />
            ))}
        </div>
    );
}
```

* 컴포넌트 랜더링
```
function Hello({ name }}) {
    return <h1>Hello {name}</h1>;
}

const studyName = [
    {
        id: 1,
        name: "insik"
    },
    {
        id: 2,
        name: "jack"
    },
    {
        id: 3,
        name: "julia"
    },
    {
        id: 4,
        name: "june"
    },
    {
        id: 5,
        name: "lewis"
    },
    {
        id: 6,
        name: "evelyn"
    }
]

function renderName(names) {
    return <Hello key={names.id} name={names.name} />
}

function App() {
    return (
        <div>{studyName.map(renderName)}</div>
    );
}
```

* Protection with PropTypes
```
function Hello({ name }}) {
    return <h1>Hello {name}</h1>;
}

const studyName = [
    {
        id: 1,
        name: "insik"
    },
    {
        id: 2,
        name: "jack"
    },
    {
        id: 3,
        name: "julia"
    },
    {
        id: 4,
        name: "june"
    },
    {
        id: 5,
        name: "lewis"
    },
    {
        id: 6,
        name: "evelyn"
    }
]

function renderName(names) {
    return <Hello key={names.id} name={names.name} />
}

function App() {
    return (
        <div>{studyName.map(renderName)}</div>
    );
}
```