<template lang="">
  <div class="form-control">
    <label for="type">Тип блока</label>
    <select
      class="select"
      id="type"
        @change="changeOption"
        :value="modelValue"
      >
      <option value="title">Заголовок</option>
      <option value="subtitle">Подзаголовок</option>
      <option value="avatar">Аватар</option>
      <option value="text">Текст</option>
    </select>
  </div>
</template>
<script>
export default {
  emits: ['update:modelValue'],
  props: {
    modelValue: String,
  },
  methods: {
    changeOption(event) {
      this.$emit("update:modelValue", event.target.value)
    }
  }
}
</script>
<style lang="">
</style>