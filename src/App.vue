<template>
  <div id="app">
    <form @submit.prevent="submit">
      <div class="mt">
        <label for="name-input">氏名</label>
        <input
          type="text"
          v-model="state.name"
          id="name-input"
        />
      </div>

      <div class="mt">
        <label for="age-input">年齢</label>
        <input
          type="number"
          v-model="state.age"
          id="age-input"
        />
      </div>

      <div class="mt">
        <label for="birth-input">生年月日</label>
        <input
          type="date"
          v-model="state.birthDay"
          id="birth-input"
        />
      </div>

      <div class="mt">
        <label for="profile-input">プロフィール</label>
        <textarea
          v-model="state.profile"
          rows="4"
          cols="40"
          id="profile-input"
        ></textarea>
      </div>

      <div class="mt">
        <label for="tel-input">電話番号</label>
        <input
          type="text"
          v-model="state.telNumber"
          id="tel-input"
        />
      </div>

      <div class="mt">
        <label for="address-input">都道府県</label>
        <select
          v-model="state.address"
        >
          <option>都</option>
          <option>道</option>
          <option>府</option>
          <option>県</option>
        </select>
      </div>

      <div class="mt">
        <input type="submit"/>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import {defineComponent, reactive} from '@vue/composition-api'

type State = {
  name: string;
  age: number;
  birthDay: Date;
  profile: string;
  telNumber: string;
  address: string;
}

export default defineComponent({
  setup() {
    const state = reactive<State>({
      name: "name",
      age: 20,
      birthDay: new Date(),
      profile: "",
      telNumber: "",
      address: "都"
    });

    function submit() {
      alert('called submit')
    }

    return {
      state,
      submit
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.mt {
  margin-top: 20px;
}
</style>
