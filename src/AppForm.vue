<template lang="">
    <form class="card card-w30" @submit.prevent="setInputData">

      <app-select v-model="currentOption"></app-select>

      <app-input v-model="inputData"></app-input>

      <app-button @setData="setData"></app-button>

    </form>

</template>
<script>
import AppButton from "./AppButton"
import AppInput from "./AppInput"
import AppSelect from "./AppSelect"

export default {
  data() {
    return {
      inputData: "",
      currentOption: "title"
    }
  },
  methods: {
    setInputData() {
      this.$emit('pass-data', {
        option: this.currentOption,
        input: this.inputData
      })
      this.currentOption = 'title'
      this.inputData = ""
    },
  },
  components: {
    AppButton,
    AppInput,
    AppSelect,
  }
}
</script>
