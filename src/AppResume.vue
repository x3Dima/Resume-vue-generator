<template lang="">
    <app-wrap v-if="isEmpty" >
      <h3>Добавте первый блок, чтобы увидеть результат</h3>
    </app-wrap>

    <app-wrap v-else>
      <app-header>{{ this.userName }}</app-header>

      <app-avatar :src="this.imagePath"></app-avatar>

      <app-about
        v-for="item in aboutArray"
        :key="item"
        :item="item"
        ></app-about>
    </app-wrap>
</template>
<script>
import AppHeader from "./AppHeader"
import AppAvatar from "./AppAvatar"
import AppAbout from "./AppAbout"
import AppWrap from "./AppWrap"


export default {
  props: {
    isEmpty: Boolean,
    userName: String,
    imagePath: String,
    aboutArray: [],
  },
  components: {
    AppHeader,
    AppAvatar,
    AppAbout,
    AppWrap,
  }
}
</script>
<style lang="">

</style>