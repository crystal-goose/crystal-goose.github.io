---
layout: base
title: redux thunk fetch logic, test ...
---

# redux thunk fetch logic

使用redux thunk发起异步请求，一般典型的模式是这样的

1. dispatch fetch request action.
2. if fetch succeed, return fetch success action
3. if fetch fails, return fetch failure action

In the action creator, we could do this:

```javascript
export function fetchTodos() {
  return dispatch => {
    dispatch(fetchTodosRequest())
    return fetch('http://example.com/todos')
      .then(res => res.json())
      .then(body => dispatch(fetchTodosSuccess(body)))
      .catch(ex => dispatch(fetchTodosFailure(ex)))
  }
}
```
在action creator中处理请求 -> 成功/失败的逻辑。

在component当中也可以实现这个逻辑，不过有些繁琐。因为action creator返回的就是一个promise。另外这种模式其实是boilerplate。

# Action creator 测试方法

测试方法如下。Mock API 请求，Mock store。然后调用action creator，检查 store 中收到的 action 是否符合预期。


在进行async action creator的测试时，可以使用fetch mock。jest里似乎也有类似的mock，不需要使用fetch mock.

```javascript
import configureMockStore from 'redux-mock-store'
import thunk from 'redux-thunk'
import * as actions from '../../actions/TodoActions'
import * as types from '../../constants/ActionTypes'
import fetchMock from 'fetch-mock'
import expect from 'expect' // You can use any testing library
​
const middlewares = [thunk]
const mockStore = configureMockStore(middlewares)
​
describe('async actions', () => {
  afterEach(() => {
    fetchMock.reset()
    fetchMock.restore()
  })
​
  it('creates FETCH_TODOS_SUCCESS when fetching todos has been done', () => {
    fetchMock
      .getOnce('/todos', { body: { todos: ['do something'] }, headers: { 'content-type': 'application/json' } })
​
​
    const expectedActions = [
      { type: types.FETCH_TODOS_REQUEST },
      { type: types.FETCH_TODOS_SUCCESS, body: { todos: ['do something'] } }
    ]
    const store = mockStore({ todos: [] })
​
    return store.dispatch(actions.fetchTodos()).then(() => {
      // return of async actions
      expect(store.getActions()).toEqual(expectedActions)
    })
  })
})
```

# Reducer 的测试方法

比较简单。Give state, action, verify new state is as expected

# Component测试
## Dumb component的测试

检查是否渲染了需要的组件
检查组件是否有需要的css class.
检查组件接收到的props内容是否正确。
可以直接调用props中的函数，然后检查期望的回调函数是否被触发（使用 jest.fn()可以对props中的函数进行mock，检查函数是否被调用）。

## Connected component的测试

可以用<Provider>提供真实的store.

建议将Dumb Component也 export 出来。

# Jest snapshot
用于确保回归是原有功能不收影响，这个是最好的办法了。

因为snapshot不处理event和props，所以这些还是需要测试的。

