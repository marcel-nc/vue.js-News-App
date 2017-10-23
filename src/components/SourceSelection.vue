<template>
  <div class="sourceselection">
    <div>
      <div class="container">
        <span>Select News</span>
        <select class="custom-select" required v-on:change="sourceChanged">
          <option value="">Select News</option>
          <option v-for="source in sources" v-bind:value="source.id">{{source.name}}</option>
        </select>
        <div v-if="source">
          <div class="jumbotron jumbotron-fluid">
            <div class="posleft">
              <p>{{source.description}}</p>
              <a v-bind:href="source.url" type="button" class="btn btn-dark" target="_blank">Visit {{source.name}}</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'sourceselection',
  data () {
    return {
      sources: [],
      source: ''
    }
  },
  
  created: function () {
    this.$http.get('https://newsapi.org/v1/sources?language=en')
      .then(response => {
        this.sources = response.data.sources;
      });
  },

  methods: {
    sourceChanged: function(e) {
     for (var i=0; i<this.sources.length; i++) {
       if (this.sources[i].id == e.target.value) {
         this.source = this.sources[i];
       }
     }
     this.$emit('sourceChanged', e.target.value);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.posleft{
  margin-left: 25%;
}
</style>