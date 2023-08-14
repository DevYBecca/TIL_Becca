## React.Fragment

> - React에서 JSX 코드를 작성할 때, 여러 개의 요소를 반환하려면 하나의 부모 요소로 묶어줘야 하고 이 때 사용하는 것이 `Fragment`
> - `Fragment`를 사용하여 불필요한 DOM 요소를 추가하지 않고 여러 요소를 그룹화 할 수 있음
> - React 16 ver.부터는 Fragments를 `<>...</>` 형태의 단축 구문을 사용할 수 있음
> - 전통적인 문법은 `<React.Fragment>...</React.Fragment>`
>   - `React.Fragment`는 명시적으로 Fragment를 나타낼 수 있음
>   - map() 함수 등을 사용하여 `key 값을 속성에 지정`해줘야 한다면, `React.Fragment를 사용`해야 함, 단축 Fragment에는 속성 지정 불가!
> - 장점
>   - 불필요한 DOM 노드의 생성을 막아 **메모리를 적게 사용**
>   - css에서 특별한 부모-자식 관계를 가지고 있는 **flexbox(display: flex;)나 gridbox에서 element 사이에 <div>를 추가하게 되면 레이아웃을 유지하기 어려워**지므로 fragment를 사용하기

<br />
