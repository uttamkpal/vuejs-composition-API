<script setup>
import { computed, reactive, ref } from 'vue';

const isSee = ref(false)
const type = "A"
const parentMessage = ref('Parent')
const items = ref([{ message: 'item' }, { message: 'item_' }])


/* items.forEach((item, index) => {
  // has access to outer scope `parentMessage`
  // but `item` and `index` are only available in here
  console.log(parentMessage, item.message, index)
}) */

const myObject = reactive({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10'
})

const numbers = ref([1, 2, 3, 4, 5, 7, 6, 8, 9])

const evenNumbers = computed(() => {
  return numbers.value.filter((n) => n % 2 === 0)
})
const sets = ref([
  [1, 2, 3, 4, 5],
  [6, 7, 8, 9, 10]
])

function even(numbers) {
  return numbers.filter((number) => number % 2 === 0)
}
</script>
<template>
    <div>
        <button @click="isSee = !isSee">Toggle</button>
        <p v-if="isSee">isSee is true so we can see this</p>
        <!-- <p v-if="!isSee">isSee is false so we can see this. Here use ! (not) oparetor</p> -->
        <p v-else>isSee is false so we can see this. Here use ! (not) oparetor</p>
        <p v-if="!isSee">isSee is false so we can see this. Here use ! (not) oparetor</p>

        <div v-if="type === 'A'">
        A
        </div>
        <div v-else-if="type === 'B'">
        B
        </div>
        <div v-else-if="type === 'C'">
        C
        </div>
        <div v-else>
        Not A/B/C
        </div>
    </div>
    <div>
        <h2>v-for List Rendering</h2>
        <ul>
            <li v-for="{ message } in items">
            {{ message }}
            </li>

            <!-- with index alias -->
            <li v-for="({ message }, index) in items">
            {{ message }} {{ index + 1 }}
            </li>
        </ul>

        <ul>
  <li v-for="(value , key) in myObject" >
    {{ key }} : {{ value }}
  </li>
  <li v-for="(value , key, index) in myObject" >
    {{ index }} - {{ key }} : {{ value }} 
  </li>
</ul>

<!-- <MyComponent
  v-for="(item, index) in items"
  :item="item"
  :index="index"
  :key="item.id"
/> -->
        <h1>v-if and v-for in same element</h1>
        <div>v-if not work so we can see title</div>
        <li v-for="(item , key) in myObject" v-if="key != 'title'">
        {{ item }}
        </li>
        <h3>Solution : This can be fixed by moving v-for to a wrapping template tag (which is also more explicit):</h3>
        <template v-for="(item , key) in myObject">
            <li v-if="key != 'title'">
                {{ item }} 
            </li>
        </template>
        <h3>evenNumbers</h3>
        <div v-for="evenNumber of evenNumbers">
            {{ evenNumber }}
        </div>
        <ol v-for="numbers in sets">
            <li v-for="n in even(numbers)">{{ n }}</li>
        </ol>
    </div>
</template>
<style>

</style>
