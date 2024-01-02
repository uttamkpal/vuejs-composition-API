<script setup>
import { computed, nextTick, reactive, ref } from 'vue'

var count = ref(1)
console.log(count)
console.log(count.value)
count.value++
console.log(count.value)

async function increment() {
  count.value++
  await nextTick()
}
async function decrement() {
  count.value--
  await nextTick()
}
const obj = ref({
  nested: { count: 0 },
  arr: ['name', 'age']
})
function mutateDeeply() {
  obj.value.nested.count++
  obj.value.arr.push(Math.round(Math.random(1, 100) * 100))
}
const state = reactive({ name: 'Uttam Kumar Pal' })

const firstName = ref('Uttam')
const lastName = ref('Kumar')

const fullName = computed({
  // getter
  get() {
    return firstName.value + ' ' + lastName.value
  },
  // setter
  set(newValue) {
    // Note: we are using destructuring assignment syntax here.
    ;[firstName.value, lastName.value] = newValue.split(' ')
  }
})
const ok = true

const classObject = reactive({
  test: true,
  'text-danger': false
})
const active = ref(false)

const activeColor = ref('red')
const fontSize = ref(30)
const styleObject = reactive({
  color: 'red',
  fontSize: '13px'
})
</script>

<template>
  <div>
    {{ count }}
    <br />
    <button @click="increment">++</button>
    <button @click="decrement">--</button>
    <br />
    {{ obj }}
    <br />
    <button @click="mutateDeeply">update obj</button>
    <br />
    <div :style="{ color: activeColor, fontSize: fontSize + 'px' }">Here use inline style</div>
    <div :style="styleObject">Here use inline style by object form</div>
    <br />
    <div @click="active = !active" :class="[active ? 'test' : 'btn']">click for update</div>
  </div>
  <div>
    <p :class="classObject">My name is {{ state.name }}</p>
    <button @click="state.name = 'Name is changed'">Change my name</button>
  </div>
  <div>
    <h2 class="container" :class="{ test: ok }">
      Computed Properties: {{ fullName }} <br />
      <button @click="fullName = 'Name changed'" :class="{ btn: ok }">change name</button>
    </h2>
  </div>
  <div>
    <p>objects, arrays, or JavaScript built-in data structures like Map via ref().</p>
    <p>Non-primitive values are turned into reactive proxies via reactive()</p>
    <div>
      <h2>Limitations of reactive()</h2>
      <ol>
        <li>
          <b>Limited value types:</b> it only works for object types (objects, arrays, and
          collection types such as Map and Set). It cannot hold primitive types such as string,
          number or boolean.
        </li>
        <li>
          <b>Cannot replace entire object:</b> since Vue's reactivity tracking works over property
          access, we must always keep the same reference to the reactive object. This means we can't
          easily "replace" a reactive object because the reactivity connection to the first
          reference is lost:
          <br />
          <code>
            <pre>
            let state = reactive({ count: 0 })

            // the above reference ({ count: 0 }) is no longer being tracked
            // (reactivity connection is lost!)
            state = reactive({ count: 1 })
          </pre
            >
          </code>
        </li>
        <li>
          <b>Not destructure-friendly:</b> when we destructure a reactive object's primitive type
          property into local variables, or when we pass that property into a function, we will lose
          the reactivity connection: <br />
          <code>
            <pre>
            const state = reactive({ count: 0 })

            // count is disconnected from state.count when destructured.
            let { count } = state
            // does not affect original state
            count++

            // the function receives a plain number and
            // won't be able to track changes to state.count
            // we have to pass the entire object in to retain reactivity
            callSomeFunction(state.count)
          </pre
            >
          </code>
        </li>
      </ol>
      <div>
        Due to these limitations, we recommend using ref() as the primary API for declaring reactive
        state.
      </div>
    </div>
  </div>
</template>

<style>
.container {
  width: 70%;
  margin: 0 auto;
}
.btn {
  background-color: blue;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
}
.test {
  font-size: 30px;
  color: red;
}
</style>
