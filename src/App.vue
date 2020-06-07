<template>
  <div id="app">
    <form @submit.prevent="submit">
      <div class="mt">
        <label for="name-input">氏名</label>
        <input
          type="text"
          v-model="form.name.$value"
          id="name-input"
        />
      </div>

      <div class="mt">
        <label for="age-input">年齢</label>
        <input
          type="number"
          v-model="form.age.$value"
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
          v-model="form.profile.$value"
          rows="4"
          cols="40"
          id="profile-input"
        ></textarea>
      </div>

      <div class="mt">
        <label for="tel-input">電話番号(ハイフン含)</label>
        <input
          type="text"
          v-model="form.telNumber.$value"
          id="tel-input"
        />
      </div>

      <div class="mt">
        <label for="address-input">都道府県</label>
        <select
          v-model="state.address"
          id="address-input"
        >
          <option>都</option>
          <option>道</option>
          <option>府</option>
          <option>県</option>
        </select>
      </div>

      <div class="mt">
        <input
          :disabled="form.$anyInvalid"
          type="submit"
        />
      </div>

      <div>
        <p v-if="form.name.$anyInvalid">氏名: {{form.name.$message}}</p>
        <p v-if="form.age.$anyInvalid">年齢: {{form.age.$message}}</p>
        <p v-if="form.birthday.$anyInvalid">生年月日: {{form.birthday.$message}}</p>
        <p v-if="form.profile.$anyInvalid">プロフィール: {{form.profile.$message}}</p>
        <p v-if="form.telNumber.$anyInvalid">電話番号: {{form.telNumber.required.$message}} {{form.telNumber.format.$message}}</p>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import {defineComponent, reactive} from '@vue/composition-api'
import {useValidation} from 'vue-composable'

type State = {
  name: string;
  age: number;
  birthDay: Date;
  profile: string;
  telNumber: string;
  address: string;
}

const required = x => !!x
const numerically = v => {
  return v.match(/\d+/)
};
const telNumberFormat = v => {
  return v.match(/\d{2,3}-\d{1,4}-\d{4}$/)
}

export default defineComponent({
  setup() {
    const state = reactive<State>({
      name: "",
      age: 20,
      birthDay: new Date(),
      profile: "",
      telNumber: "",
      address: "都"
    });

    const form = useValidation({
      name: {
        $value: state.name,
        required,
        $message: "必須項目です"
      },
      age: {
        $value: state.age,
        numerically,
        $message: "数値を入力してください"
      },
      birthday: {
        $value: state.birthDay,
        required,
        $message: "必須項目です"
      },
      profile: {
        $value: state.profile,
        required,
        $message: "必須項目です"
      },
      telNumber: {
        $value: state.telNumber,
        required: {
          $validator: required,
          $message: "必須項目です"
        },
        format: {
          $validator: telNumberFormat,
          $message: "電話番号の形式が不正です"
        }
      }
    })

    function submit() {
      alert('called submit')
    }

    return {
      state,
      form,
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
