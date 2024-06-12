# 지현수 202030331
## 6월 12일 강의

# 1 .CSS란 ?

- CSS (Cascading style sheets)
- cascading ? 계단식 이란 뜻으로 한 엘리먼트에 여러 스타일이 적용될 경우 스타일간의 충돌을 막기 위해 계단식으로 스타일을 적용시키는 규칙을 갖고 있음
- 하나의 스타일이 여러 개의 엘리먼트에 적용될 수 있고, 하나의 엘리먼트에도 여러 개의 스타일이 적용될 수 있음
- 엘리먼트에 스타일이 적용되는 규칙을 selector(선택자)라고 함. css는 이 선택자와 스타일로 이루어져 있음

# 2. 레이아웃과 관련된 속성

- 화면에 엘리먼트를 어떻게 배치할 것인지 정의
- _가장 중요한 속성 ->`display`_
- `none` -> 존재하지만 화면에 보이지 않음
- `block` -> 세로로 정렬. width와 height를 가질 수 있음
- `inline` -> 가로로 정렬. width와 height를 가질 수 없음

- flex는 컨테이너의 형태로 엘리먼트를 관리
- 최근엔 2차원 적으로 관리가 가능한 Grid 사용

- _`visiblity` -> 엘리먼트의 가시성 정의_

- display: none - 엘리먼트의 영역이 보이지 않음
- visiblity:hidden - 차지하는 영역은 보임

# 3. styled-components

- css 문법을 그대로 사용하면서 결과물을 스타일링된 컴포넌트 형태로 만들어 주는 오픈소스 라이브러리
- 컴포넌트 개녑을 사용하고 있어 리액트 개발에 많이 사용됨

```js
const Wrapper = styled.div`
  padding: 1em;
  background: gray;
`;

const Title = styled.h1`
  font-size: 1.5rem;
  color: white;
  text-align: center;
`;

const Button = styled.button`
  color: ${(props) => (props.dark ? "white" : "black")};
  background: ${(props) => (props.dark ? "black" : "white")};
  border: 1px solid black;
`;
```
## 06월 11일 강의 내용
# Specialization (특수화, 전문화)
- 웰컴다이얼로그는 다이얼로그의 특별한 케이스입니다.
- 범용적인 개념을 구별되게 구체화하는 것을 특수화라고 합니다
- 객체지향 언어에서는 상속을 사용하여 특수화를 구현합니다.
- 리액트에서는 합성을 사용하여 특수화를 구현합니다.
- 특수화는 범용적으로 쓸 수 있는 컴포넌트를 만들어 놓고 이를 특수한 목적으로 사용하는 합성 방식

# Containment와 Specialization을 같이 사용하기.
- Containment를 위해서 props.children을 사용하고, Specialization을 위해 직접 정의한 props를 사용하면 됩니다.
- Dialog컴포넌트는 이전의 것과 비슷한데 Containment를 위해 끝부분에 props.children을 추가했습니다.
- Dialog를 사용하는 SignUpDialog는 Specialization을 위해 props인 title, message에 값을 넣어주고 있고, 입력을 받기위해 `<input>`과 `<button>`을 사용합니다. 이 두개의 태그는 모두 props.children으로 전달되어 다이얼로그에 표시됩니다.
- 이러한 형채로 Contianment와 Specialization을 동시에 사용할 수 있습니다.

# 상속에 대해 알아보기
- 합성과 대비되는 개념으로 상송(Inheritance)이 있습니다.
- 자식 클래스는 부모클래스가 가진 변수나 함수 등의 속성을 보여준다.
- 리액트에서는 상속이라는 방법을 사용하는 것보다는 합성을 사용하는 것이 더 좋음.

# 컨텍스트란 무엇인가?
- 기존의 일반적인 리액트에서는 데이터가 컴포넌트의 props를 통해 부모에서 자식으로 단방향으로 전달되었습니다.
- 컨텍스트는 리액트 컴포넌트들 사이에서 데이터를 기존의 props를 통해 전달하는 방식 대신 '컴포넌트 트리를 통해 곧바로 컴포넌트에 전달하는 새로운 방식'을 제공합니다.
- 이것을 통해 어떤 컴포넌트라도 쉽게 데이터에 접근할 수 있습니다.
- 컨텍스트를 사용하면 일일이 props로 전달할 필요 없이 그림처럼 데이터를 필요로 하는 컴포넌트에 곧바로 데이터를 전달할 수 있습니다.

# 컨텍스트를 언제 사용해야 할까?
- 여러 컴포넌트에서 자주 필요로 하는 데이터는 로그인 여부, 로그인 정보, UI테마, 현재 선택된 언어등이 있습니다.
- props를 통해 데이터를 전달하는 기존 방식은 실제 데이터를 필요로 하는 컴포넌트까지의 깊이가 깊어질 수록 복잡해집니다.
- 또한 반복적인 코드를 게쏙해서 작성해 주어야 하기 때문에 비효율적이고 가독성이 떨어집니다.
- 컨텍스트를 사용하면 이러한 방식을 깔끔하게 개선할 수 있습니다.
- 컨텍스트를 사용하려면 컴포넌트의 상위 컴포넌트에서 Provider로 감싸주어야 합니다.

``` jsx

const ThemeContext = React.createContext('light')

function App() {
    return(
        <ThemeContext.Provider value='dark'>
            <Toolbar/>
        </ThemeContext.Provider>
    )
}
function Toolbar() {
    return (
        <div>
            <ThemeButton/>
        </div>
    )
}

function ThemeButton(props) {
    return(
        <ThemeContext.Consumer>
            {value => <Button theme={value} />}
        </ThemeContext.Consumer>
    )
}
```

# 컨텍스트를 사용하기 전에 고려할 점
- 컨텍스트는 다른 레벨의 많은 컴포넌트가 특정 데이터를 필요로 하는 경우에 주로 사용합니다.
- 하지만 무조건 컨텍스트를 사용하는 것은 좋은 것은 아닙니다. 왜냐하면 컴포넌트와 컨텍스트가 연동되면 재사용성이 떨어지기 때문입니다.
- 따라서 다른 레벨의 많은 컴포넌트가 데이터를 필요로 하는 경우가 아니면 props를 통해 데이터를 전달하는 컴포넌트 합성 방법이 더 적합합니다.
- 데이터가 많아질수록 상위 컴포넌트가 점점 더 복잡해지기 때문입니다.
- 이런 경우 하위 컴포넌트를 여러 개의 변수로 나눠서 전달하면 됩니다.
- 하지만 어떤 경우에는 하나의 데이터에 다양한 레벨에 있는 중첩된 컴포넌트들의 접근이 필요할 수 있습니다. 이런 경우 컨텍스트가 유리합니다.
- 컨텍스트는 해당 데이터와 데이터의 변경사항을 모두 하위 컴포넌트들에게 broadcast해주기 때문입니다.
- 컨텍스트를 사용하기에 적합한 데이터의 대표적인 에로는 '지역 정보', 'UI테마' 그리고 '캐싱된 데이터' 등이 있습니다.

# 컨텍스트 API
1. React.createContext
- 컨텍스트를 생성하기 위한 함수 입니다.
- 파라메타에는 기본값을 넣어주면 됩니다.
- 하위 컴포넌트는 가장 가까운 상위 레벨의 Provider로 부터 컨텍스트를 받게 되지만, 만일 Provider를 찾을 수 없다면 위에서 설정한 초기값을 사용하게 됩니다.
``` jsx
const MyContext = React.createContext(초기값);
```

2. Context.Provider
- Context.Provider 컴포넌트로 하위 컴포넌트들을 감싸주면 모든 하위 컴포넌트들이 해당 컨텍스트의 데이터에 접근할 수 있게 됩니다.
``` jsx
<MyContext.Provider value={/-some value-/}>
```
- Provider(제공자) 컴포넌트에는 value라는 prop이 있고, 이것은 Provider 컴포넌트 하위에 있는 컴포넌트에게 전달됩니다.
- 하위 컴포넌트를 consumer(소비자) 컴포넌트라고 부릅니다.

3. Context.Consumer 
- 함수형 컴포넌트에서 COntext.Consumer를 사용하여 컨텍스트를 구독 할 수 있습니다.
``` jsx
<MyContext.Consumer>
    {value => /*컨텍스트의 값에 따라서 컴포넌트들을 렌더링*/}
</MyContext.Consumer>
```
- 컴포넌트의 자식으로 함수가 올 수 있는데 이것을 function as a child라고 부릅니다.
- Context.Consumer로 감싸주면 자식으로 들어간 함수가 현재 컨텍스트의 value를 받아서 리액트 노드로 리턴합니다.
- 함수로 전달되는 value는 Provider의 value prop과 **동일**합니다

4. Context.displayName
- 컨텍스트 객체는 displayName이라는 문자열 속성을 갖습니다.
- 크롬의 리액트 개발자 도구에서는 컨텍스트의 Provider나 Consumer를 표시할 때 displayName을 함께 표시해줍니다.
``` jsx
const MyContext = React.createContext(/*some value*/);
MyContext.displayName = 'MyDisplayName';

// 개발자 도구에 "MyDisplayName.Provider"로 표시됨
<MyContext.Provider>

// 개발자 도구에 "MyDisplayName.Consumer"로 표시됨
<MyContext.Consumer>
```

### 여러 개의 컨텍스트 사용하기
- 여러 개의 컨텍스트를 동시에 사용하려면 Context.Provider를 중첩해서 사용합니다.
- 하지만 두개 또는 그 이상의 컨텍스트 값이 자주 함께 사용될 경우 모든 값을 한 번에 제공해주는 별도의 render prop 컴포넌트를 직접 만드는 것을 고려하는 것이 좋습니다.

### useContext
- 함수형 컴포넌트에서는 컨텍스트를 사용하기 위해 컴포넌트를 매번 Consumer 컴포넌트로 감싸주는 것보다 더 좋은 방법이 있습니다. 바로 Hook입니다.
- useContext() 훅은 React.createContext() 함수 호출로 생성된 컨텍스트 객체를 인자로 받아서 현재 컨텍스트 값을 리턴합니다.
``` jsx
function MyComponent(props) {
    const value =useContext(MyContext);
    return(
        ...
    )
}
```
- 이 방법도 가장 가까운 상위 Provider로 부터 컨텍스트의 값을 받아옵니다.
- 만일 값이 변경되면 useContext() 훅을 사용하는 컴포넌트가 재 렌더링 됩니다.
- 또한 useContext() 훅을 사용할 때에는 파라미터 컨텍스트로 객체를 넘겨줘야 된다.
``` jsx
// 올바른 사용법
useContect(MyContext)

// 잘못된 사용법
useContext(MyContext.Provider)
useContext(MyContext.Consumer)
```
## 06월 05일 강의 내용
- shared state는 state의 공유를 의미합니다.
- 같은 부모 컴포넌트의 state를 자식 컴포넌트가 공유해서 사용하는 것입니다.
- 입력 컴포넌트 추출하기
```jsx
import { useState } from "react";
import BoilingVerdict from "./BoilingVerdict";

export default function Calculator() {
    const [temperature, setTemperrature] = useState('')
    const handleChange = (e) => {
        setTemperrature(e.target.value)
    }

    return(
        <fieldset>
            <legend>섭씨 온도를 입력하세요</legend>
            <input type="number" value={temperature}
            onChange={handleChange} />
            <BoilingVerdict celsius={parseFloat(temperature)} />
        </fieldset>
    )
}
```
- 이렇게 하는 이유는 용도에 따라 입력을 받을 수 있도록 해서 재사용이 가능하게 하기 위해서입니다.

### shared State 적용하기
- 다음은 하위 컴포넌트의 state를 부모 컴포넌트로 올려서 shared state를 적용합니다.
이것을 Lifting State Up (State 끌어 올리기)라고 합니다.
- 이를 위해 먼저 TemperatureInput 컴포넌트에서 온도 값을 가져오는 부분을 다음과 같이 수정합니다.
- 이렇게 수정하면 온도를 state에서 가져오지 않고 props를 통해 가져옵니다.
``` jsx
export default function TemperatureInput(props) {
    //const [temperature, setTemperature] = useState('')
    const handleChange = (e) => {
        //setTemperature(e.target.value)
        props.onTemperatureChange(e.target.value)
    }
        return(
        <fieldset>
            <legend>섭씨 온도를 입력하세요(단위: {scaleName[props.scale]})</legend>
            {/* <input type="number" value={temperature}
            onChange={handleChange} /> */}
            <input type="number" value={props.temperature}
            onChange={handleChange} />
        </fieldset>
    )
}
```
- 또 한가지 컴포넌트의 state를 사용하지 않기 때문에
입력 값이 변경되었을 때 상위 컴포넌트로 변경된 값을 전달해 주어야 합니다.
 이를 위해 handler함수를 다음과 같이 수정해줍니다.
- 최종 코드는 다음과 같이 state는 제거되고, 상위 컴포넌트에서 전달받은 값만 사용합니다.
- 상위 컴포넌트인 Calculator에서 온도와 단위를 state로 갖고
- 두개의 하위 컴포넌트는 각각 섭씨, 화씨로 변환된 온도와 단위, 그리고 온도를 업데이트하기 위한 함수를 props로 갖고 있습니다
- 이렇게 모든 컴포넌트가 state를 갖지 않고, 상위 컴포넌트만 

### 합성에 대해 알아보기
- 합성(Compostion)은 여러 개의 컴포넌트를 합쳐서 새로운 컴포넌트를 만드는 것입니다.
- 조합 방법에 따라 합서의 사용 기법은 다음과 같이 나눌 수 있습니다.
1. Containment(담다, 포함하다, 격리하다)
    - 특정 컴포넌트가 하위 컴포넌트를 포함하는 형태의 합성 방법입니다.
    - 컴포넌트에 따라서는 어떤 자식 엘리먼트가 들어올지 미리 예상할 수 없는 경우가 있습니다.
    - 범용적인 박스 역할을 하는 Sidebar 혹은 Dialog와 같은 컴포넌트에서 특히 자주 볼 수 있습니다.
    - 이런 컴포넌트에서는 children prop을 사용하여 자식 엘리먼트를 출력에 그대로 전달하는 것이 좋습니다.
    - 이때 children prop은 컴포넌트의 props에 기본적으로 들어있는 children속성을 사용합니다. 
    - 리엑트에서는 props, children을 통해 하위 컴포넌트를 하나로 모아서 제공해줍니다.
    - 만일 여러 개의 chidren 집합이 필요할 경우에도 별도로 props를 정의해서 각각 원하는 컴포넌트를 넣어줍니다.
## 5월 29일 강의내용  
# select태그  
- 드롭다운(drop-down) 목록을 보여주기 위한 HTML 태그  
- 여러 가지 옵션 중에서 하나를 선택할 수 있는 기능을 제공
- HTML 에서는 아래 코드와 같이 태그를 태그가 감싸는 형태로 사용
- 현재 선택된 옵션의 경우 `selected`라는 `attribute`를 가지고 있음  
```jsx
<select>
    <option value="apple">사과</option>
    <option value="banana">바나나</option>
    <option selected value="grape">포도</option>
    <option value="watermelon">수박</option>
</select>
```  

# Input Null Value
- 앞에서 배운 것 처럼 제어 컴포넌트에 value prop을 정해진 값으로 넣으면 코드를 수정하지 않는 한 입력값을 바꿀 수 없다.  
- 만약 value prop은 넣되 자유롭게 입력할 수 있게 만들고 싶다면 앞에 undefined 또는 null을 넣어주면 된다.  
- 아래 코드를 예로 들면, 처음에는 input 값이 hi로 정해져있어서 값을 바꿀 수 없는 입력 불가 상태였다가 timer에 의해 1초 뒤에 value가 null인 input 태그가 렌더링되면서 입력 가능한 상태로 바뀐다.

```jsx
    ReactDOM.render(<input value="hi" />, rootNode);

    setTime(function() {
        ReactDOM.render(<input value={null} />, rootNode);
    }, 1000);
```

- 이러한 방법을 잘 활용하면 value prop을 넣으면서 동시에 사용자가 자유롭게 입력할 수 있게 만들 수 있다.

## 실습코드
```jsx
    import React, { useState } from "react";

function SignUp(props) {
    const [name, setName] = useState("");
    const [gender, setGender] = useState("남자");

    const handleChangeName = (event) => {
        setName(event.target.value);
    };

    const handleChangeGender = (event) => {
        setGender(event.target.value);
    };

    const handleSubmit = (event) => {
        alert(`이름: ${name}, 성별: ${gender}`);
        event.preventDefault();
    };

    return (
        <form onSubmit={handleSubmit}>
            <label>
                이름:
                <input type="text" value={name} onChange={handleChangeName} />
            </label>
            <br />
            <label>
                성별:
                <select value={gender} onChange={handleChangeGender}>
                    <option value="남자">남자</option>
                    <option value="여자">여자</option>
                </select>
            </label>
            <button type="submit">제출</button>
        </form>
    );
}

export default SignUp;
```
## 5월 22일 강의내용  
# 리스트와 키  
- 리스트는 자바스크립트의 변수나 객체를 하나의 변수로 묶어 놓은 배열과 같은 것입니다.  

- 다음은 리액트에서 map()함수를 사용한 예제입니다  
```jsx
const numbers = [1,2,3,4,5];
const listItems = numbers.map((number) => 
    <li>{numbers}</li>
);

```
- 리스트는 같은 아이템을 순서대로 모아 놓은 것이다.  
- 키는 각 객체나 아이템을 구분할 수 있는 고유한 값이다.  
- 여러 개의 컴포넌트를 렌더링하기 위해서는 map()함수를 사용한다.  
- 키 값을 사용하는 방법에는 숫자 값, id, 인덱스를 사용하는 방법이 있다.   
- 리액트에서는 키를 명시적으로 넣어주지 않으면 기본적으로 인덱스 값을 키값으로 가진다.
# 키값
- 숫자 *(인덱스)* 값
- id *(고유 값)* 값
- 포맷팅된 문자열
```jsx
<li key={`student-${stu.type}-${stu.id}`}>{stu.name}</li>
```

# 리액트 form 태크
제어태그

# 기본적인 리스트 컴포넌트
- NumberList 컴포넌트는 props로 숫자가 들어있는 배열인 numbers를 받아서 이를 목록으로 출력한다.
- 하지만 현재 각 아이템에 아직 키가 없기 때문에 콘솔창에는 리스트 아이템에는 무조건 키가 있어야 한다는 경고 문구가 출력된다.  

# 키값으로 index 사용하기
- map() 함수에서 두 번째 파라미터로 제공해주는 인덱스 값을 키값으로 사용  
- 인덱스도 고유한 값이기 때문에 키값으로 사용해도 되지만 배열에서 아이템의 순서가 바뀔수 있는 경우에는 사용하면 안됨  
- 리액트에서는 키를 명시적으로 넣어주지 않으면 기본적으로 인덱스 값을 키값으로 사용  

```jsx
const todoItems = todos.map((todo, index) => {
  	// 아이템의 고유한 ID 가 없을 경우에만 사용
    <li key={index}>
        {todo.text}
    </li>
});
```

## 5월 8일 강의 내용
# 이벤트 처리하기
리액트에서 이벤트 이름은 **카멜 케이스** 사용  
ex) ```onClick``` *(javascript와 다르니 주의)*  

이벤트 핸들러 *(이벤트 리스너)* 는 함수 실행 형태가 아니라 함수 그 자체를 전달
```jsx
<button onClick={handleClick} />
```

# 이벤트 핸들러 추가하기
1. 함수안에 함수로 정의하기
```jsx
function handleClick(){
    // ... To do
}
```

2. arrow function을 사용해서 정의
```jsx
const handleClick = () => {
    // ... To do
}
```

# arguments 전달하기
- 함수를 정의할 때는 파라미터 혹은 매개변수,  
  함수를 사룡할때는 아귀먼트 혹은 인수라고 부릅니다.
- 이벤트 핸들러에 매개변수를 전달해야 하는 경우도 많습니다.  



### 리엑트 이벤트 객체 전달받기
```jsx
<button onClick={(event) => handleDelete("흠흐밍", event)} />
```

### 조건부 렌더링
조건에 따라서 return 하는(렌더링되는) 컴포넌트가 달라지는 것
```jsx
function Greeting(props){
    const isLogin = pros.isLogin

    if(isLogin) {
        return <UserGreeting />
    }
    return <LoginButton />
}
```


### 엘리먼트 변수
렌더링해야 될 컴포넌트를 변수처럼 사용하는 방법
```jsx
let button;
if(isLogin) button = <button onClick={handleLogoutClick}>로그아웃</button>
else button = <button onClick={handleLoginClick}>로그인</button>

return (
    <div>
        <div>코드...</div>
        {button}
    </div>
)
```

### 인라인 조건
1. 인라인 if  
  - if문을 사용하지 않고 논리 연산자(&&)를 사용  
  - &&는 and연산자로 모든 조건이 참일때만 참이 됩니다.  
  - 첫 번 조건이 거짓이면 두번째 조건은 판단할 필요가 없습니다.  
  ```jsx
  {
    unreadMessages.length > 0 &&
    <h2>현재 {unreadMessages.length}개의 읽지 않은 메세지가 있습니다
  }
  ```
  앞에게 false면 뒤에것을 검사하지 않는 특성을 사용 *(단축평가)*

2. 인라인 if-else  
  - 삼항 연산자를 사용합니다.  
  - 문자열이나 엘리먼트를 넣어서 사용할 수도 있습니다.
  ```jsx
  <div>
    { isLogin ? <Logoutbutton /> : <LoginButton /> }
  </div>
  ```


### 컴포넌트 null 리턴(렌더링 막기)  
- 컴포넌트를 렌더링하고 싶지 않을때는 null 리턴
```jsx
    function WaringBanner(props){
        if(!props.warning){
            return null;
        }

        return(
            <div>경고!</div>
        );
    }
```

## 5월 1일 강의
# 이벤트 처리
* DOM에서 클릭 이벤트를 처리하는 예제 코드
``` jsx
<button onClick="activate()">
    Activate
</button>
```
* React에서 클릭 이벤트 처리하는 예제 코드
``` jsx
<button onClick={activate}>
    Activate
</button>
```
* 둘의 차이점은
    1. 이벤트 이름이 onclick에서 onClick으로 변경
    2. 전달하려는 함수는 문자열에서 함수 그대로 전달
* 이벤트가 발생했을 때 해당 이벤트를 처리하는 함수를 '이벤트 핸들러'라고 합니다. 또는 이벤트가 발생하는 것을 계속 듣고 있다는 의미로 '이벤트 리스너'라고 부르기도 합니다.

# 커스텀 훅
* 필요하다면 직접 훅을 만들어 사용할 수 있음. 이것을 `커스텀 훅`이라고 합니다
1. `use`로 시작해야된다. 그렇지 않으면 다른 훅을 불러올 수 없습니다
2. 훅 함수 안에 중복됐던 함수를 그대로 넣음
3. 리턴 값은 훅에서 사용했던 값만 
4. 일반 컴포넌트와 마찬가지로 다른 훅을 호출하는 것은 무조건 커스텀 훅의 최상위 레벨에서만 해야 합니다.

## 4월 17일 강의
# 훅
* 클래스형 컴포넌트에서는 생성자에서 state를 정의하고, setState() 함수를 통해 state를 업데이트합니다.
* 함수형 컴포넌트에서도 state나 생명주기 함수의 기능을 사용하게 해주기 위해서 추가도니 기능이 바로 훅(Hook)입니다.
* `Hook`이란 <U> state와 생명주기 기능에 갈고리를 걸어 원하는 시점에 정해진 함수를 실행되도록 만든 함수</U>를 의미합니다.
* 훅의 이름은 모두 `'use'`로 시작하며, 사용자 정의 훅을 만들 수 있고 이름은 자유롭게 사용할 수 있으나 `'use'`로 시작할 것을 권장.

# useState
* `useState`는 함수형 컴포넌트에서 state를 사용하기 위한 Hook입니다.
* 다음 예제는 버튼을 클릭했을 때 카운트가 증가하는 함수형 컴포넌트 입니다. 증가시킬 수 있지만 증가할 때마다 재 렌더링은 일어나지 않습니다. 즉 화면에 값이 바로 반영되지 않기 때문에 useState를 사용
* 이럴 때 state를 사용해야 하지만 함수형에는 없기 때문에 useState()를 사용합니다.


``` jsx
import React, {useState} from "react"

export default function Counter(props) {
    const [count, setCount] = useState(0)
  
    return (
        <div>
        <p>총 {count}번 클릭했습니다.</p>
        <button onClick={() => setCount(count+1)}>클릭</button>
        </div>
    )
}
const [변수, set(함수)] = useState(초기값) 구조분해할당
0번 인덱스에 변수와 setter 지정
```
# useEffect
* useState와 함께 가장 많이 사용하는 Hook입니다.
* 이 함수는 사이드 이펙트를 수행하기 위한 것입니다.
* 영어로 side effect는 부작용을 의미합니다. 일반적으로 프로그래밍에서 사이트 이펙트는  '개발자가 의도하지 않은 코드가 실행되면서 버그가 발생하는 것'을 말합니다.
* 이 작업을 이펙트라고 부르는 이유는 이 작업들의 다른 컴포넌트에 영향을 미칠 수 있으며, <U>렌더링 중에는 작업이 완료될 수 없기 때문</U>이다. 렌더링이 끝난 이후에 실행되어야 하는 작업들이다.
* <U>클래스 컴포넌트의 생명주기 함수와 같은 기능을 하나로 통합한 기능</U>을 제공합니다.  

* 사이드 이펙트는 렌더링 외에 실행해야 하는 부수적인 코드를 말합니다. 예를 들면 네트워크 리퀘스트, DOM수동조작, 로깅 등은 정리가 필요없는 경우들입니다.
* useEffect()함수
``` jsx
useEffect(이펙트함수, 의존성 배열)
```
* 첫 번째 파라미터는 <u>이펙트 함수</u>가 들어가고, 두 번째 파라미터로는 <u>의존성 배열</u>이 들어갑니다.
* 의존성 배열은 이펙트가 의존하고 있는 배열로, <u>배열 안에 있는 변수 중에 하나라도 값이 변경되었을 때 이펙트 함수가 실행</u>됩니다.
* 이펙트 함수는 <u>처음 컴포넌트가 렌더링 된 이후</U>, 그리구 <u>재 렌더링 이후</u>에 실행됩니다.
* 만약 이펙트 함수가 마운트와 언마운트 될 때만 한 번씩 실행되게 하고 싶으면 빈 배열을 넣으면 됩니다. 이 경우 props나 state에 있는 어떤 값에도 의존하지 않기 떄문에 여러 번 실행되지 않습니다.

# useMemo
* useMemo() 혹은 Memoizde value를 리턴하는 훅입니다.
* 이전 계산값을 갖고 있기 때문에 연산량이 많은 작업의 반복들 피할 수 있습니다.
* 이 훅은 렌더링이 일어나는 동안 실행됩니다. 따라서 렌더링이 일어나는 동안 실행되서는 안될 작업을 넣으면 안됩니다.
* 예를 들면 useEffect에서 실행되어야 할 사이드 이펙트 같은 것입니다.
``` jsx
const memoizedValue = useMemo(
    () => {
        //연산량이 높은 작업을 수행하여 결과를 반환
        return computeExpensiveValue(의존성 변수1, 의존성 변수2);
    },
    [의존성 변수1, 의존성 변수2]
)
```
``` jsx
const memoizedValue = useMemo(
    () => computeExpensiveValue(a, b)
);
```
* 다음 코드와 같이 의존성 배열을 넣지 않을 경우, 렌더링이 일어날 때마다 매번 함수가 실행됩니다. 따라서 의존성 배열을 넣지 않는 것은 의미가 없습니다.
* 만약 빈 배열을 넣게 되면 컴포넌트 마운트 시에만 함수가 실행됩니다.

# useCallback
* useCallback() 훅은 useMemo()와 유사합니다. 차이점은 값이 아닌 함수를 반환한다는 것입니다.
* 의존성 배열을 파라미터로 받는 것은 useMemo와 같습니다

# useRef
* useRef() 훅은 레퍼런스를 사용하기 위한 훅입니다.
* 레퍼런스란 특정 컴포넌트에 접근할 수 있는 객체를 의미합니다.
* useRef() 훅은 바로 이 레퍼런스 객체를 반환합니다.
* 레퍼런스 객체에는 .current라는 속성이 있는데, 이것은 현재 참조하고 있는 엘리먼트를 의미합니다.
``` jsx
const refContainer = useRef(초깃값);
```
* 이렇게 반환된 레퍼런스 객체는 컴포넌트의 라이프타임 전체에 걸쳐서 유지됩니다. 즉, 컴포넌트가 마운트 해제 전까지는 계속 유지된다는 의미입니다.
``` jsx
import React, {useRef} from "react"

export default function FocusButton() {
    const inputElem = useRef(null)

    const onButtonClick = () => {
        inputElem.current.focus()
    }
    return (
        <div>
            <input ref={inputElem} type="text" />
            <button onClick={onButtonClick}>Focus the input</button>
        </div>
    )
}
```

# 훅의 규칙
* 첫 번째 규칙은 무조건 최상의 레벨에서만 호출해야 한다는 것입니다. 여기서 최상위는 컴포넌트의 최상위 레벨을 의미합니다. 따라서 반복문이나 조건문 또는 중첩된 함수들 안에서 훅을 호출하면 안됩니다.
* 이 규칙에 따라서 훅은 컴포넌트가 렌더링 될 때마다 같은 순서로 호출되어야 합니다.
* 두 번째 규칙은 리액트 함수형 컴포넌트에서만 훅을 호출해야 한다는 것입니다. 따라서 일반 자바스크립트 함수에서 훅을 호출하면 안됩니다.


## 4월 3일 강의
# Props 사용법  
JSX에서는 key-value쌍으로 props를 구성합니다.  

JSX를 사용하지 않는 경우 props의 전달 방법은 createElement()함수를 사용하는것입니다.



```js
React.createElement(
    type,
    [props],
    [...children]
)

```
# 컴포넌트 만들기
1. 컴포넌트의 종류  
- 리액트 초기 버전을 사용할 때는 클래스형 컴포넌트를 주로 사용했습니다.  
- 이후 Hook이라는 개념이 나오면서 최근에는 함수형 컴포넌트를 주로 사용합니다.  
- 예전에 작성된 코드나 문서들이 클래스형 컴포넌트를 사용하고 있기 때문에,  
- 클래스형 컴포넌트와 컴포넌트의 생명주기에 관해서도 공부해 두어야 합니다.  

2. 함수형 컴포넌트  
- Welcome컴포넌트는 props를 받아, 받은 props중 name키의 값을 "안녕."뒤에 넣어 반환합니다


```js
funtion Welcome(props){
    return <h1>안녕, {props.name} <h1>;
}

conse element = <Welcome name="인제" />;
ReactDOM.render(
    element,
    document.getElementById('root')
);

```

4. 컴포넌트 이름 짓기
- 이름은 항상 대문자로 시작합니다.  
- 왜냐하면 리액트는 소문자로 시작하는 컴포넌트를 DOM태그로 인식하기 때문입니다. html tag.  
- 컴포넌트 파일 이름과 컴포넌트 이름은 같게 합니다.

# 컴포넌트 합성  
- 컴포넌트 합성은 여러 개의 컴포넌트를 합쳐서 하나의 컴포넌트를 만드는 것입니다.  
- 리액트에서는 컴포넌트 안에 또 다른 컴포넌트를 사용할 수 있기 때문에, 복잡한 화면을 여러개의 컴포넌트로 나누어 구현할 수 있습니다.

# 컴포넌트 추출  
- 복잡한 컴포넌트를 쪼개서 여러 개의 컴포넌트로 나눌 수도 있습니다.  
- 큰 컴포넌트에서 일부를 추출해서 새로운 컴포넌트를 만드는 것입니다.  
- 두 번째로 사용자 정보 부분을 추출합니다.  
- 컴포넌트 이름은 UserInfo로 합니다. React 컴포넌트 이름은 Camel notaion을 사용합니다.  
- UserInfo 안에 Avatar 컴포넌트를 넣어서 완성시킵니다.  

```js
function UserInfo(props){
    return (
        <div className="user-info">
            <Avatar user={props.user}/>
            <div className="user-info-name">
                {props.user.name}
            </div>  
        </div>
    );    
}
```
# State
1. state란?  
- State는 리액트 컴포넌트의 상태를 의미합니다.  
- 상태의 의미는 정상인지 비정상인지가 아니라 컴포넌트의 데이터를 의미합니다.  
- 정확히는 컴포넌트의 변경가능한 데이터를 의미합니다.  
- State가 변하면 다시 렌더링이 되기 때문에 렌더링과 관련된 값만 state에 포함시켜야 합니다.  

2. state의 특징  
- 리액트만의 특별한 형태가 아닌 단지 자바스크립트 객체일 뿐입니다.  
- 예의 LikeButton은 class 컴포넌트입니다.  
- constructor는 생성자이고 그 안에 있는 this.state가 현 컴포넌트의 state입니다.  

*함수형 에서는 useState()라는 함수를 사용합니다.

## 3월 27일 강의
# 컴포넌트에 대해 알아보기  
- 리액트는 컴포넌트 기반의 구조를 갖습니다.
- 컴포넌트 구조라는 것은 작은 컴포넌트가 모여 큰 컴포넌트를 구성하고, 다시 이런 컴포넌트들이 모여서 전체 페이지를 구성한다는 것을 의미합니다.  
- 컴포넌트 재사용이 가능하기 때문에 전체 코드의 양을 줄일 수 있어 개발 시간과 유지 보수 비용도 줄일 수 있습니다.
- 컴포넌트는 자바스크립트 함수와 입력과 출력이 있다는 면에서는 유사합니다.
- 다만 입력과 출력은 입력은 Props가 담당하고, 출력은 리액트 엘리먼트의 형태로 출력됩니다.
- 엘리먼트를 필요한 만큼 만들어 사용한다는 면에서는 객체 지향의 개념과 비슷합니다.dd

# Props의 개념  
- props 는 prop의 준말입니다.
- 이 props가 바로 컴포넌트의 속성입니다.  
- 컴포넌트에 어떤 속성, props를 넣느냐에 따라서 속성이 다른 엘리먼트가 출력됩니다.  
- props는 컴포넌트에 전달 할 다양한 정보를 담고 있는 자바스크립트 객체입니다.  
- 에어비앤비의 예도 마찬가지 입니다.  

# Props의 특징  
- 읽기 전용입니다. 변경할 수 없다는 의미 입니다.  
- 속성이 다른 엘리먼트를 생성하려면 새로운 props를 컴포넌트에 전달하면 됩니다.  

Pure 함수 vs Impure 함수  
- Pure함수는 인수로 받은 정보가 함수 내부에서도 변하지 않는 함수입니다.  
- Impure함수는 인수로 받는 정보가 함수 내부에서 변하는 함수 입니다.  
```js
//pure 함수
//input을 변경하지 않으며 같은 input에 대해서 항상 같은 output을 리턴
function sun(a,b){
    return a+b;
}
```
```js
//impure 함수
//input울 변경함
function withdraw(account, amount){
    account.total -= amount;
}
```



# JSX의 역할  
-JSX는 내부적으로 XML/HTML 코드를 자바스크립트로 변환합니다.  
-React 가 createElement함수를 사용하여 자동으로 자바스크립트로 변환해 줍니다.  
-만일 JS로 작업할 경우 직접 createElement함수를 사용해야 합니다.  
-앞으로 설명하는 코드를 보면 알 수 있지만 결국 JSX는 가독성을 높여 주는 역할을 합니다.  

## JSX의 장점  
-코드가 간결해 집니다.  
-가독성이 향상 됩니다.  
-Injection Attack이라 불리는 해킹 방법을 방어함으로써 보안에 강합니다.  

## JSX 사용법
-모든 자바스크립트 문법을 지원합니다.  
-자바 스크립트 문법에 XML과 HTML을 섞어서 사용합니다.
-만일 html이나 xml에 자바스크립트 코드를 사용하고 싶으면 {}괄호를 사용합니다.


## 엘리먼트에 대해 알아보기  
#1. 엘리먼트의 정의  
-엘리먼트는 리액트 앱을 구성하는 요소를 의미합니다.
-공식페이지에는 "엘리먼트는 리액트 앱의 가장 작은 빌딩 블록들" 이라고 설명하고 있습니다.  
-웹사이트의 경우는 DOM엘리먼트이며 HTML요소를 의미합니다.  

----리액트 엘리먼트와 DOM엘리먼트는 어떤 차이가 있을까?  
-리액트 엘리먼트는 Virtual DOM의 형태를 취하고 있습니다.  
-DOM 엘리먼트는 페이지의 모든 정보를 갖고 있어 무겁습니다.  
-반면 리액트 엘리먼트는 변화한 부분만 갖고 있어 가볍습니다.

# 2. 엘리먼트의 생김새
- 리액트 엘리먼트는 자바스크립트 객체의 형태로 존재합니다.  
- 컴포넌트(Button 등), 속성(color 등) 및 내부의 모든 children을 포함하는 일반 JS객체입니다.  
- 이 객체는 마음대로 변경할 수 없는 불변성을 갖고 있습니다.  
- 리액트 엘리먼트의 예를 보면 type에 태그 대신 리액트 컴포넌트가 들어가 있는 것 외에는 차이가 없다는 것을 알 수 있습니다.
- 역시 자바스크립트 객체입니다.
```js
{
    type: Button,
    props: {
        color: 'green',
        children: 'hello, element!'
    }   
}
```
내부적으로 자바스크립트 객체를 만드는 역할을 하는 함수가 createElement()입니다,
- 첫 번째 매개변수가 type입니다. 이 곳에 태그가 들어가면 그대로 표현하고, 만일 리액트 컴포넌트가 들어가면 이 것을 분해해 결국 태그로 만들게 됩니다.  
- 두 번째 매개변수인 props는 속성을 나타냅니다.  
- 세 번째 매개변수는 children입니다. 

# 3.엘리먼트의 특징  
리액트 엘리먼트의 가장 큰 특징은 불변성입니다.
즉. 한 번 생성된 엘리먼트의 children이나 속성을 바꿀 수 없습니다.

만일 내용이 바뀌면 어떻게 해야 할까요?

- 이 때는 컴포넌트를 통해 새로운 엘리먼트를 생성하면 됩니다.  
- 그 다음 이전 엘리먼트와 교체를 하는 방법으로 내용을 바꾸는 것입니다.  
- 이렇게 교체하는 작업을 하기 위해 virtual DOM을 사용합니다.  

다음은 html코드는 id값이 root인 div태그로 단순하지만 리액트에 필수로 들어가는 아주 주용한 코드입니다. 이 div태그 안에 리액트 엘리먼트가 렌더링 되며, 이것을 Root DOM node라고 합니다.

```js
    <div id = 'root'></div>
```
엘리먼트를 렌더링 하기 위해서는 다음과 같은 코드가 필요합니다.  

```js
const element = <h1>안녕, 리액트!</h1>;
ReactDOM.render(element, document.getElementById('root'));
```





## 3월 20일 강의
# 리액트의 장점 
1. 빠른 업데이트와 렌더링 속도  
    -이 것을 가능하게 하는 것이 바로 Virtual DOM입니다.  
    -DOM이란 XML, HTML 문서의 각 항목을 계층으로 표현하여 생성,변형,삭제할 수 있도록 돕는 인터페이스 입니다.
    -Virtual DOM은 DOM조작이 비효율적인 이유로 속도가 느리기 때문에 고안된 방법입니다.  
    -DOM은 동기식, Virtual DOM은 비동기식으로 렌더링을 합니다.

2.  컴포넌트 기반 구조  
    -리액트의 모든 페이지는 컴포넌트로 구성됩니다.  
    -하나의 컴포넌트는 다른 여러 개의 컴포넌트의 조합으로 구성할 수 있습니다.  
    -그래서 리액트로 개발을 하다 보면 레고 블록을 조립하는 것처럼 컴포넌트를 조합해서 웹사이트를 개발하게 됩니다.

4. 든든한 지원군  
    -메타(구 페이스북)에서 오픈소스 프로젝트로 관리하고 있어 계속 발전하고 있습니다.

5. 활발한 지식 공유 & 커뮤니티  

6. 모바일 앱 개발기능  
    -리액트 네이티브 라는 모바일 환경 UI프레임워크를 사용하면 크로스 플랫폼(cross-platform)가능

# 리액트의 단점  
1. 방대한 학습량
    자바스크립트를 공부한 경우 빠르게 학습할 수 있습니다.
2. 높은 상태 관리 복잡도
    state, component life cycle 등의 개념이 있지만 그리 어렵지 않습니다.
    
            
## 3월 13일 강의
```

```
## 3월 6일 강의
# h1
## h2
### h3
#### h4
##### h5
###### h6


# 리스트
1. 첫 번째
2. 두 번째
3. 세 번째

* 첫 번째
* 두 번째

*이탈릭체*
**굵게**
***두개합침***

일반 문장을  
쓸데도 마찬가지

```
```

[구글링크](http://google.net)  
[페이지 내 링크](#리스트)

![리트리버 인절미](/dang.jpg)

---
