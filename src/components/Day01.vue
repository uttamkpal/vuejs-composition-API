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
const classTest = 'test'
const ok = ref(true)
const num = [1,2,3,4,5]
const url = ref('/')
const attributeName = ref("href")
const eventName = ref('click')
</script>

<template>
  <!-- <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
      </nav>
    </div>
  </header> -->
  <div v-bind="objectOfAttrs">
    <div :class="classTest">{{ ok ? "Yes it is OK" : "No it is not OK" }} <span class="btn"  @click="ok = !ok">change ok </span> 
     <div>
      <div>
        <a :href="url">go to home</a> <br>
        <a v-bind:[attributeName]="`${url}/nothing`">{{attributeName}}</a>
        <br>
        <button @[eventName]="attributeName= 'nothing'">{{attributeName}}</button>
        <br>
        <a :[attributeName]="url"> {{ url }} </a>
      </div>
      <p v-if="ok">This is show when OK is true</p>
      
      <!--{{ massage.split('').reverse().join('') }}-->
    </div> 
    <div>
      <h3 v-for="item in num" :id="`id-number-${item}`">{{ item }}</h3>
    </div>
    </div>

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

  
  <form @submit.prevent="onSubmit">...</form>
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
.btn{
  background-color: blue;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
}
.test{
  font-size: 30px;
  color: red;
}
</style>
