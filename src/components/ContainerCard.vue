<template>
  <div>
      <div class="bg-top-bar">
          <div class="container">
              <div class="header">

                <h1>Boolflix</h1>
                <SearchBar @textSearch="saveTextSearch" />
              </div>
          </div>
      </div>
      <main>
        <Card :film="arrayFilm" :series="arraySeries" :flags="flags" />
      </main>
  </div>
</template>

<script>
import axios from "axios"
import SearchBar from "./SearchBar.vue"
import Card from './Card.vue'
export default {
    name: "ContainerCard",
    data(){
        return {
            apiKey: "0265c53357a1868741506ffbd3f187b5",
            apiUrl: "https://api.themoviedb.org/3",
            arrayFilm: [],
            arraySeries: [],
            textQuery: "",
            flags: {
                it: "https://images.emojiterra.com/twitter/v13.1/512px/1f1ee-1f1f9.png",
                en: "https://images.emojiterra.com/twitter/v13.1/512px/1f3f4-e0067-e0062-e0065-e006e-e0067-e007f.png",
                es: "https://images.emojiterra.com/twitter/v13.1/512px/1f1ea-1f1f8.png",
                jp: "https://images.emojiterra.com/twitter/v13.1/512px/1f1ef-1f1f5.png",
                de: "https://images.emojiterra.com/twitter/v13.1/512px/1f1e9-1f1ea.png",
                fr: "https://images.emojiterra.com/twitter/v13.1/512px/1f1eb-1f1f7.png",
                br: "https://images.emojiterra.com/twitter/v13.1/512px/1f1e7-1f1f7.png",
                ch: "https://images.emojiterra.com/twitter/v13.1/512px/1f1e8-1f1ed.png",
                dk: "https://images.emojiterra.com/twitter/v13.1/512px/1f1e9-1f1f0.png",
                gr: "https://images.emojiterra.com/twitter/v13.1/512px/1f1ec-1f1f7.png",
                kr: "https://images.emojiterra.com/twitter/v13.1/512px/1f1f0-1f1f7.png",
                pl: "https://images.emojiterra.com/twitter/v13.1/512px/1f1f5-1f1f1.png",
                ar: "https://images.emojiterra.com/twitter/v13.1/512px/1f1e6-1f1f7.png",
            }
        }
    },
    components:{
        SearchBar,
        Card,
    },

    methods: {
        saveTextSearch(textSearch){
            this.textQuery = textSearch

            this.callAxios("/search/movie")
            this.callAxios("/search/tv")
        },

        callAxios(url){
            axios.get(this.apiUrl + url, {
                params: {
                    api_key: this.apiKey,
                    query: this.textQuery,
                    language: "it-IT"
                }
            }).then((resp) => {
                if (url.includes("movie")) {
                    this.arrayFilm = resp.data.results
                }else{
                    this.arraySeries = resp.data.results
                }
            })
        }
    },

    mounted() {
    }
}
</script>

<style lang="scss">

.bg-top-bar{
    background-color: #303030;
}
.header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    
    h1{
        color: #e50914;
    }
}
main{
    background-color: black;
}

</style>