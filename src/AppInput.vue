<template lang="">
  <div class="form-control">
    <label for="value">Значение</label>
    <textarea
    id="value"
    :value="modelValue"
    @input="inputData"
    rows="3"></textarea>
  </div>
</template>
<script>
export default {
  emits: ['update:modelValue'],
  props: {
    modelValue: String,
  },
  methods: {
    inputData(event) {
      this.$emit("update:modelValue", event.target.value)
    }
  }
}
</script>
<style lang="">
</style>
