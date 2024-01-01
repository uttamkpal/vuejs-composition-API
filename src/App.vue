<script setup>
import { onMounted, ref } from 'vue'

const massage = ref('HI there this is Uttam kumar pal')
const count = ref(0)
function Increment() {
  count.value++
}
function Decrement() {
  count.value--
}

onMounted(() => {
  count.value = 3
  console.log('Vue js in running in this page')
})
const htmlText = '<p> This is a Html Text with red color.</p>';

const idList = {
  id : "test"
}
const id = ref('test')
const objectOfAttrs = {
  id: 'container',
  class: 'wrapper'
}
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <!-- <RouterLink to="/">Home</RouterLink> -->
      </nav>
    </div>
  </header>
  <div v-bind="objectOfAttrs">
    <h1>
    {{ massage }}
    </h1>
    <!-- <div v-bind="idList" v-html="htmlText"></div> -->
    <div :id="id" v-html="htmlText"></div>
    <button @click="id='something'">change Id test to something</button>

    <h1>Count is : {{ count }}</h1>
    <!-- <button @click="count++">
      Increment Count
    </button> -->
    <button @click="Increment">+</button>
    <!-- <button @click="count--">
      Decrement Count
    </button> -->
    <button @click="Decrement">-</button>
  </div>

  

  <!-- <RouterView /> -->
</template>

<style>
#container{
  width: 70%;
  margin: 0 auto;
}
  #test{
    font-size: 30px;
    color: red;
  }
  #something{
    font-size: 20px;
    color: green;
  }
</style>
