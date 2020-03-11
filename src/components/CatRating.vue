<template>
    <div>
        <div v-if="loading"><img id="loading-gif" src="../../public/images/loading.gif"></div>
        <div id="images-to-rate" v-else>
            <img :src="this.cat.url" alt="" id="image-to-rate" class="cat-image">
            <div id="buttons" class="button-container">
                <img src="../../public/images/like.png" @click="liked()">
                <img src="../../public/images/dislike.png" @click="notLiked()">
            </div>
        </div>
        <div>U HAVE LIKED {{ likedCats }} CATZ!</div>
        <div>...BUT U DID NOT LIKE {{ notLikedCats }} CATZ!</div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "CattoRating",
  data () {
      return {
          cat: null,
          loading: true,
          likedCats: 0,
          notLikedCats: 0
      }
  },
  created () {
      this.getCat()
  },
  methods: {
      getCat () {
          axios.defaults.headers.common['x-api-key'] = '574f7140-45cb-40bb-98ac-e6f8ea43fc3f';
          axios.get('https://api.thecatapi.com/v1/images/search', { params: { limit: 1, size: "full" } } )
          .then(response => {
              this.cat = response.data[0];
              this.loading = false;
          })
      },
      liked () {
          this.likedCats++;
          this.loading = true;
          this.getCat();
      },
      notLiked () {
          this.notLikedCats++;
          this.loading = true;
          this.getCat();
      }
    }
};
</script>
    
<style scoped>
    img#image-to-rate {
        height: 50vh;
    }

    img#loading-gif {
        height: 50vh;
    }

    div#buttons {
        display: grid;
        grid-template-columns: auto auto;
        justify-content: space-evenly;
    }

    div#buttons img {
        cursor: pointer;
        height: 10vh;
        margin: 2rem;
    }

    #images-to-rate {
        display: inline-grid;
    }
</style>