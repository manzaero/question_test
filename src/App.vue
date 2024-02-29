<template>
  <div class="main">
    <div class="header">
      <div class="user">
        <div class="name">Anton</div>
        <div class="energy">
          <span>1000</span>
          <img src="@/assets/img/coin.png" alt="">
        </div>
      </div>
    </div>

    <div class="title">
      <button>
        <img src="@/assets/img/close_btn.png" alt="">
      </button>
      <h4>
        {{ questions.question }}
      </h4>
      <button @click="open = true">
        <img src="@/assets/img/bulb.png" alt="">
      </button>
    </div>

    <div class="question">
      <h3>
        {{ questions.title }}
      </h3>
    </div>

    <div class="question_image">
      <img :src="questions.picture" alt="">
    </div>

    <div>
      <h4>Result: {{resultCheck}}</h4>
    </div>

  </div>
  <div class="footer row">
    <div
        class="btn-radio col-sm"
        v-for="item in questions.answer"
        :key="item.id"
    >
      <input type="radio" class="btn-check" name="options"
             :value="item.value"
             v-model="radioCheck"
             :disabled="isDisabledRadio()"
      >
      <label class="btn btn-secondary" for="label">
        {{item.option}}
      </label>
    </div>



    <div class="btn-radio col-sm">
      <button @click="result" class="btn btn-exam btn-success" :disabled="isDisabledBtn()">Check</button>
    </div>

  </div>

  <div v-if="open" class="modal">
    <div class="modal__p">
      <p>Hello from the modal!</p>
      <button @click="open = false">Close</button>
    </div>
  </div>
</template>


<script setup>
import {reactive, ref} from "vue";
const open = ref(false);
import data from "./data.json"

const radioCheck = ref('');
const resultCheck = ref()
const questions = reactive(data)

const result = () => {
  if (radioCheck.value === false){
    resultCheck.value = 'false'
  } else {
    resultCheck.value = 'true'
  }
}

const isDisabledRadio = () => {
  if (resultCheck.value) return true
}

const isDisabledBtn = () => {
  if (radioCheck.value === '') return true
}



</script>


<style scoped lang="scss">
.modal {
  position: fixed;
  z-index: 999;
  top: 0;
  width: 100%;
  height: 100%;
  margin-left: -0.4%;
  text-align: center;
  background-color: rgba(117, 156, 184, 0.7);
  &__p {
    margin-top: 20%;
    font-size: 30px;
    button {
      margin-top: 5%;
      width: 100px;
      height: 30px;
    }
  }
}
* {
  margin: 0;
  padding: 0;
}
.main {
  position: relative;
  max-width: 1200px;
  margin: 80px auto 0;
  min-height: calc(100vh - 148px);
}
.header {
  display: flex;
  justify-content: right;
}
.energy span {
  margin-right: 6px;
}
.title {
  display: flex;
  justify-content: space-around;
  margin-top: 100px;
}
.question {
  display: flex;
  justify-content: center;
  &_image {
    display: flex;
    justify-content: center;
    margin-top: 200px;
  }
}
.footer {
  display: flex;
  justify-content: space-between;
  background-color: #D3D3D3;
  padding: 20px;
}
.btn {
  width: 280px;
}
.btn-exam {
  min-width: 280px;
}
button {
  cursor: pointer;
}
</style>
