<template>

  <div class="container column" >
    <form class="card card-w30" @submit.prevent="">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select
          class="select"
          id="type"
          @change="changeOption"
          v-model="currentOption"
          >
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" ref="userData" rows="3"></textarea>
      </div>

      <button
        class="btn primary"
        v-if="currentOption === 'title'"
        @click="setName"
        >Добавить</button>

      <button
        class="btn primary"
        v-else-if="currentOption === 'avatar'"
        @click="setAvatar"
        >Добавить</button>

        <button
        class="btn primary"
        v-else-if="currentOption === 'subtitle'"
        @click="setSubtitle"
        >Добавить</button>

        <button
        class="btn primary"
        v-else-if="currentOption === 'text'"
        @click="setText"
        >Добавить</button>

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


export default {
  props: ["src"],
  data() {
    return {
      isEmpty: true,
      userName: "",
      currentOption: 'title',
      aboutArray: [],
      imagePath: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTugu0kegXOT1Gh1sgDVHvYjkGW29w19Hl9gQ&usqp=CAU"
    }
  },
  methods: {
    setName() {
      if(this.$refs.userData.value.length) {
        this.isEmpty = false
      }
      this.userName = this.$refs.userData.value
      this.$refs.userData.value = ""
      this.currentOption = "title"
    },
    setAvatar() {
      if(this.$refs.userData.value.length) {
        this.isEmpty = false
      }
      this.imagePath = this.$refs.userData.value
      this.$refs.userData.value = ""
      this.currentOption = "title"
    },
    setSubtitle() {
      if(this.$refs.userData.value.length) {
        this.isEmpty = false

      let subtitle = {
        text: this.$refs.userData.value,
        type: "h2"
       }
        this.aboutArray.push(subtitle)
      }
      this.$refs.userData.value = ""
      this.currentOption = "title"
    },
    setText() {
      if(this.$refs.userData.value.length ) {
        this.isEmpty = false

      let text = {
        text: this.$refs.userData.value,
        type: "p"
       }
       this.aboutArray.push(text)
      }
      this.$refs.userData.value = ""
      this.currentOption = "title"
    },
    load() {
      this.isLoad = true
    }
  },
  components: {
    AppHeader,
    AppAvatar,
    AppComments,
    AppAbout,
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
