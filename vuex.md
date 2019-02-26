# vuex

![screenshot](./images/vuex-architecture.png)
[출처](https://vuex.vuejs.org/kr/)

- 컴포넌트가 액션을 일으킨다(버튼 클릭)
- 액션에서 외부 api호출 후 그 결과를 이용해 mutations을 일으킨다
- mutations에서 상태를 업데이트 한다(이 단계는 추적이 가능함)
- 변경된 상태는 다시 컴포넌트에 바인딩 된다.

**주의사항**
mutations의 목적은 상태의 변경
상태의 변경과 관련 없는 작업이 mutations내부에서 수행되지 않도록
또한 mutations는 동기적인 작업이므로 비동기 처리는 mutations에서 수행하지 않는다.
** state는 mutations를 통해서만 변경하도록**


전역에서 vuex사용하기
````
# cmd
npm i vuex --save

# Store 객체 생성
# src/store/index.js

import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex) // vuex를 모든 컴포넌트에서 state, mutations에 접근할 수 있도록 설정

const store = new Vuex.Store({
  state: {
    todolist: [
      {todo: '', done: false}
    ]
  },
  mutations: {
    addTodo: (state, payload) => { # addTodo : 액션 명, mutations은 2개의 매개변수를 갖는다. state,와 상태를 변이시킬 데이터
      state.todolist.push({todo: payload.todo, done: false})
    }
  }
})

export default store
----------------------------------------------

# main.js
import store from './store' # store객체 import

new Vue({
  store, # store객체 추가하여 전역에서 사용가능 하도록
  render: h => h(App)
}).$mount('#app');


----------------------------------------------

# inputTodo.vue

...

methods: {
  insertTodo(data) {
    this.$store.commit('addTodo', {todo: data}); # 전역에서 vuex를 사용할수 있으므로 this.$store.commit()로 메서드를 이용해 변이를 일으킬 수 있음
  }
}

# List.vue

export default {
  computed: {
    todoList() {
      return this.$store.state.todoList; # this.$store.state 저장소에 접근 할 수 있음, 직접적인 상태 변화를 하면 안되고 상태가 변이가 되면 자동으로 업데이트 하기위해 computed (계산형 속성을 사용, 계산형 속성은 읽기 전용)
    }
  }
}
````