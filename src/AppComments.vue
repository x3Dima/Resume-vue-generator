<template>
  <div class="container">
    <p>
      <button class="btn primary" @click="loadComments">{{loadBtnText}}</button>
    </p>

    <app-loader v-if="isLoading"></app-loader>

    <div class="card" v-if="isLoad">
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="item in comments" :key="item.id">
          <div>
            <p><strong>{{item.email}}</strong></p>
            <small>{{item.name}}</small>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import AppLoader from './AppLoader'

export default {

  data() {
    return {
      isLoad: false,
      comments: [],
      loadBtnText: 'Загрузить комментарии',
      isLoading: false,
    }
  },
  methods: {
    async loadComments() {
      if(!this.isLoad) {
        this.isLoad = true
        this.loadBtnText = 'Закрыть коментарии'
      } else {
        this.isLoad = false
        this.loadBtnText = 'Загрузить комментарии'
      }
      this.isLoading = true
      let response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=20');
      response = await response.json();
      this.isLoading = false

      this.comments = response
    }
  },
  components: {
    AppLoader,
  }
}
</script>
