<template>
  <div class="home">
    <section>
      <div class="home__blog container">
        <card 
          v-for="post in posts" :key="post.id" 
          class="home__card" :class="post.type" :_post="post"
          />
      </div>
    </section>
  </div>
</template>

<script>
import card from './../components/card.vue'

export default {
  name: 'home',
  data() {
    return {
      posts: null
    }  
  },
  methods: {
    loadData: function() { 
      this.$http.get('http://localhost:9000/api/tiles').then((response) => { 
        if(response) {
          this.posts = response.body.tiles
        }
      }, (response) => {
        console.log(response)
      })
    }
  },
  created () {
      this.loadData()
  },
  components: {
    card
  }
}
</script>

<style scoped>
.home__blog {
  justify-content: flex-start;
  display: flex;
  flex-wrap: wrap;
}
.home__card {
  color: #fff;
  background-image: url('http://placekitten.com/500/400');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
  margin: 3px 3px;
  text-shadow: 1px 1px 0px rgba(150, 150, 150, 1);
  box-shadow: 0 2px 2px 0 rgba(0,0,0,0.16), 0 0 0 1px rgba(0,0,0,0.08);
  border-radius: 2px;
}
@media (min-width: 1024px) {
  .home__card.normal {
    width: calc(33% - 3px);
  }
  .home__card.double {
    width: calc(33% * 2);
  }
 }
@media (max-width: 1024px) {
  .home__card.double {
    width: 100%;
    flex-grow: 0;
  }
  .home__card.normal {
    width: calc(50% - 6px);
    flex-grow: 0;
  }
}
@media (max-width: 480px) {
  .home__card.double,
  .home__card.normal{
    width: 100%;
  }
}
</style>
