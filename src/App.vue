<template>

  <div class="container column" >

    <form class="card card-w30" @submit.prevent="">

      <app-select v-model="currentOption"></app-select>

      <app-input v-model="userData"></app-input>

      <app-button @setData="setData"></app-button>

    </form>

    <div v-if="isEmpty" class="card card-w70">
      <h3>Добавте первый блок, чтобы увидеть результат</h3>
    </div>

    <div class="card card-w70" v-else>
      <app-header>{{ this.userName }}</app-header>

      <app-avatar :src="this.imagePath"></app-avatar>

      <app-about
        v-for="item in aboutArray"
        :key="item"
        :item="item"
        ></app-about>
    </div>
  </div>
  <app-comments></app-comments>
</template>

<script>
import AppHeader from "./AppHeader"
import AppAvatar from "./AppAvatar"
import AppComments from "./AppComments"
import AppAbout from "./AppAbout"
import AppButton from "./AppButton"
import AppInput from "./AppInput"
import AppSelect from "./AppSelect"


export default {
  props: ["src"],
  data() {
    return {
      isEmpty: true,
      userName: "",
      currentOption: 'title',
      userData: "",
      aboutArray: [],
      imagePath: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTugu0kegXOT1Gh1sgDVHvYjkGW29w19Hl9gQ&usqp=CAU"
    }
  },
  methods: {
    setData() {
      if(this.userData.length) {
        this.isEmpty = false
      }
      if(this.currentOption === 'title') {
        this.userName = this.userData
      } else if (this.currentOption === 'avatar') {
       this.imagePath = this.userData
      } else if (this.currentOption === 'subtitle') {
          let subtitle = {
          text: this.userData,
          type: "h2"
        }
          this.aboutArray.push(subtitle)
      } else if(this.currentOption === 'text') {
          let text = {
          text: this.userData,
          type: "p"
        }
        this.aboutArray.push(text)
      }

      this.userData = ""
      this.currentOption = "title"

    },
    load() {
      this.isLoad = true
    },
  },
  components: {
    AppHeader,
    AppAvatar,
    AppComments,
    AppAbout,
    AppButton,
    AppInput,
    AppSelect,
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
