<script>
const axios = require('axios');

export default {
  name: 'HelloWorld',
  data() {
    return {
      books: [],
      current: {}
    }
  },

  methods: {
    async getData() {
      let response = await axios.get('http://localhost:8080/books/all')
      this.books = response.data;
      response = await axios.get('http://localhost:8080/books/current')
      this.current = response.data;
      response = await axios.get('http://localhost:8080/books/read')
      this.booksRead = response.data;
    }
  },

  created() {
    this.getData()
  }
}
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <div v-for="book in books" :key="book._id">

          <div class="card text-white bg-dark mb-3" style="max-width: 540px;">
            <div class="row no-gutters">
              <div class="col-md-4">
                <img :src="book.image" class="card-img" alt="book-img">
              </div>
              <div class="col-md-8">
                <div class="card-body">
                  <h5 class="card-title">{{book.title}}</h5>
                  <p class="card-text">{{ book.description }}</p>
                  <p class="card-text"><small class="text-muted"><a :href="book.link" class="btn btn-primary" target="_blank">Google Livres</a></small></p>
                </div>
              </div>
            </div>
          </div>

        </div>
      </div>
      <div class="col">
        <div class="card" style="width: 25rem;">
          <img class="card-img-top" :src="current.image" alt="book-image">
          <div class="card-body">
            <h5 class="card-title">{{ current.title }}</h5>
            <a :href="current.link" class="btn btn-primary" target="_blank">Google Livres</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
