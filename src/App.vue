<template>

  <app-wrap className="container column" >

    <app-form
      @pass-data="passData"
    ></app-form>

    <app-resume
      :isEmpty="isEmpty"
      :userName="userName"
      :imagePath="imagePath"
      :aboutArray="aboutArray"
      className="card card-w70"
    ></app-resume>

  </app-wrap>
  <app-comments></app-comments>
</template>

<script>
import AppComments from "./AppComments"
import AppForm from "./AppForm"
import AppResume from "./AppResume"
import AppWrap from "./AppWrap"


export default {
  props: ["src"],
  data() {
    return {
      isEmpty: true,
      userName: "",
      aboutArray: [],
      imagePath: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTugu0kegXOT1Gh1sgDVHvYjkGW29w19Hl9gQ&usqp=CAU"
    }
  },
  methods: {
    passData(data) {
      if(data.input.length) {
        this.isEmpty = false
      }
      if(data.option === 'title') {
        this.userName = data.input
      } else if (data.option === 'avatar') {
       this.imagePath = data.input
      } else if (data.option === 'subtitle') {
          let subtitle = {
          text: data.input,
          type: "h2"
        }
          this.aboutArray.push(subtitle)
      } else if(data.option === 'text') {
          let text = {
          text: data.input,
          type: "p"
        }
        this.aboutArray.push(text)
      }
    },
    load() {
      this.isLoad = true
    },
  },
  components: {
    AppComments,
    AppForm,
    AppResume,
    AppWrap,
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