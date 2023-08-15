## Redux-toolkit non-serializable 에러

> 토이 프로젝트1 리팩토링 중 redux-toolkit에 redux-persist를 추가적으로 도입하면서 로컬에서 어마무시한 길이의 에러를 만나게 되었다.<br />

```
serializableStateInvariantMiddleware.ts:234 A non-serializable value was detected in an action, in the path: `register`. Value: ƒ register(key) {
    _pStore.dispatch({
      type: _constants__WEBPACK_IMPORTED_MODULE_0__.REGISTER,
      key: key
    });
  }
Take a look at the logic that dispatched this action:  {type: 'persist/PERSIST', register: ƒ, rehydrate: ƒ}
(See https://redux.js.org/faq/actions#why-should-type-be-a-string-or-at-least-serializable-why-should-my-action-types-be-constants)
(To allow non-serializable values see: https://redux-toolkit.js.org/usage/usage-guide#working-with-non-serializable-data)
```

> 이 에러는 `'redux의 state, action에는 직렬화가 불가능한 값을 전달할 수 없다'`는 것을 의미하는데, 여기서 `직렬화란 redux에서 값을 주고받을 때 object 형태의 값을 string 형태로 변환(JSON.stringify)하는 것`을 의미하고, `string 형태의 object를 object 형태로 되돌리는(JSON.parse) 과정을 역직렬화`라고 한다. Redux-toolkit에서 제공하는 `serializableCheck 미들웨어`는 Redux 상태를 직렬화 가능한 형태로 유지하는 것을 목적으로 하는데, action 객체에 직렬화가 불가능한 값이 포함되면 이 에러가 발생하는 것이다.<br />

```
// store.tsx
const store = configureStore({
  reducer: persistedReducer,
  devTools: process.env.NODE_ENV !== 'production',
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware({
      serializableCheck: {
        ignoredActions: [FLUSH, REHYDRATE, PAUSE, PERSIST, PURGE, REGISTER],
      },
    }),
});
```

> 나는 store.tsx 파일에서 `middleware 체크 시 무시할 action을 지정`해주는 방법으로 에러를 해결했지만 기본 값이 true로 되어있는 `serializableCheck 속성을 false로 변경`해주는 방법도 가능하다고 한다!<br />

<br />
