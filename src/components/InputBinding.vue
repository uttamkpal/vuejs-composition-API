<script setup>
import { reactive, ref } from 'vue'

const formData = reactive({
  name: 'Uttam',
  age: 18,
  gender: 'male',
  message: '',
  topic: [],
  occupation: null,
  occupation2: []
})
const selected = ref('A')

const options = ref([
  { text: 'One', value: 'A' },
  { text: 'Two', value: 'B' },
  { text: 'Three', value: 'C' }
])
</script>
<template>
  <div>
    <form action="" method="get">
      <div class="input-box">
        <label for="name">Name :</label>
        <input v-model.lazy="formData.name" type="text" id="name" placeholder="Enter name" />
        <br />
      </div>
      <div class="input-box">
        <label for="age">Age :</label>
        <input v-model.number="formData.age" type="number" id="age" />
        <br />
      </div>
      <div class="input-box">
        <label>Gender :</label>
        <input v-model="formData.gender" value="male" type="radio" id="male" /><label for="male"
          >Male</label
        >
        <input v-model="formData.gender" value="Female" type="radio" id="female" /><label
          for="female"
          >Female</label
        >
        <input v-model="formData.gender" value="Others" type="radio" id="others" /><label
          for="others"
          >Others</label
        >
        <br />
      </div>
      <div class="input-box">
        <label for="message">Message :</label>
        <textarea v-model.trim="formData.message" placeholder="Write your Message" id="message">
        </textarea>
        <br />
      </div>
      <div class="input-box">
        <label>Select Topics :</label>
        <input v-model="formData.topic" value="english" type="checkbox" id="english" /><label
          for="english"
          >English</label
        >
        <input v-model="formData.topic" value="laravel" type="checkbox" id="laravel" /><label
          for="laravel"
          >Laravel</label
        >
        <input v-model="formData.topic" value="vuejs" type="checkbox" id="vuejs" /><label
          for="vuejs"
          >Vue js</label
        >
        <br />
      </div>
      <div class="input-box">
        <label>Select Occupation :</label>
        <select v-model="formData.occupation">
          <option disabled value="null">Please select one</option>
          <option value="Student">Student</option>
          <option value="Teacher">Teacher</option>
          <option value="Business">Business</option>
          <option value="Job">Job</option>
        </select>
      </div>
      <br />
      <br />
      <div class="input-box">
        <label>Select Occupation 2 :</label>
        <select v-model="formData.occupation2" multiple>
          <option disabled value="null">Please select one</option>
          <option value="Student">Student</option>
          <option value="Teacher">Teacher</option>
          <option value="Business">Business</option>
          <option value="Job">Job</option>
        </select>
      </div>
      <select v-model="selected">
        <option v-for="option in options" :value="option.value" :key="option">
          {{ option.text }}
        </option>
      </select>

      <div>Selected: {{ selected }}</div>
      <button type="submit">Submit</button>
    </form>
    <pre>
            {{ formData }}
        </pre
    >
  </div>
</template>
