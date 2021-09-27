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

* 동적 컴포넌트
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

* PropTypes를 사용한 타입 검사
```
function Hello({ name }}) {
    return <h1>Hello {name}</h1>;
}

Hello.propTypes = {
    id: PropTypes.number.isRequired,
    name: PropTypes.string.isRequired
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
];

function renderName(names) {
    return <Hello key={names.id} name={names.name} />
}

function App() {
    return (
        <div>{studyName.map(renderName)}</div>
    );
}
```

* 클래스에 State 추가

    > set state를 호출할 때마다 react는 새로운 state와 함께 reder funtion 호출하여 다시 랜더링.
```
class App extends React.Component {
    constructor() {
        super(props);
        this.state = {
            count: 0
        };
    };
    /*
    state = {
        count: 0
    };
    */
    add = () => {
        this.setState({current => ({ count : current.count + 1 })});
    }
    minus = () => {
        this.setState({current => ({ count : current.count - 1 })});
    }
    render() {
        return (
            <div>
                <h1>Count is: {this.state.count}</h1>
                <button onClick={this.add}>Add</button>
                <button onClick={this.minus}>minus</button>
            </div>
        );
    }
}
```

* 클래스컴포넌트 생명주기

    > state에 추가되지 않아도 사용가능하지만 미래에 사용될 변수들을 미리 선언하는게 좋음.
```
class App extends React.Component {
    constructor() {
        super(props);
        this.state = {
            isLoading: true
        };
    }

    componentiDidMount() {
        setTimeout(() => {
            this.setState({ isLoading: false });
        }, 6000);
    }

    render() {
        const { isLoading } = this.state;
        return <div>{isLoading ? "Loading" : "ready"}</div>;
    }
}
```

##04. Route
* URI와 js파일을 매칭하여 랜더링
* path가 겹치는 경우 2개 js파일을 같이 랜더링
```
function App() {
  return (
    <HashRouter>
      <Route path="/" exact={true} component={default} />
      <Route path="/main" component={main} />
      <Route path="/home/:id" component={home} />
    </HashRouter>
  );
}
```
* 링크를 통해서 정보를 라우터에 전달하여 다른 컴포넌트에 전달
```
<Link to={{
    pathname: "/main",
    state: {
        id,
        name
    }
}}>
```
* 리다이렉트
```
this.props.history.push("/");
```