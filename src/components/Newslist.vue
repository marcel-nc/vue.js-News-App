<template>
  <div class="container">
    <div class="newslist">
      <li class="media" v-for="article in articles">
      <div class="card card-border" style="width: 30rem;" >
        <a v-bind:href="article.url" target="_blank">
          <img class="card-img-top" v-bind:src="article.urlToImage" alt="Card image cap">
        </a>
        <div class="card-body">
          <h4 class="media-heading"><a v-bind:href="article.url" target="_blank">{{article.title}}</a></h4>
          <h4 class="card-text"><i>by {{article.author}}</i></h4>
          <p>{{article.description}}</p>
        </div>
      </div>
      </li>
    </div>
  </div>
</template>

<script>
export default {
  name: 'newslist',
  props: ['source'],
  data () {
    return {
      articles: []
    }
  },
  methods: {
    generateView: function (source) {
      this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=9a2b802e73c94a04bf4864a6334a14bb')
       .then(response => {
         this.articles = response.data.articles;
       });   
    }
  },
  created: function () {
    this.generateView(this.source);
  },
  watch: {
    source: function (val) {
      this.generateView(val);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .media {
    margin-top: 50px;
    margin-left: 25%;

  }


.card-border{
  border: grey 2px solid;
}
</style>