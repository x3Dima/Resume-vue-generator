<template>
  <h2 v-if="item.type === 'h2'">{{item.text}}</h2>
  <p v-else>{{item.text}}</p>
</template>
<script>
export default {
  props: ['item']
}
</script>
