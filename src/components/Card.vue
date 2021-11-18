<template>
    <div>
        <div class="row">
            <div class="col">
                <h2>Film</h2>
                <div class="my-card" v-for="movie in film" :key="movie.id">
                    <img :src="selectPreview(movie.poster_path)" >
                    <div class="info-text">
                        <h6>Titolo: {{movie.title}}</h6>
                        <h6 v-if="movie.title !== movie.original_title ">Titolo originale: {{movie.original_title}}</h6>
                        <h6>Lingua: <img :src="selectFlags(movie.original_language)" alt=""></h6>
                        <h6>Voto: {{voteStarConv(movie.vote_average)}}</h6>
                    </div>
                </div>
            </div>

            <div class="col">

                <h2>Serie</h2>
                <div class="my-card" v-for="series in series" :key="series.id">
                    <img :src="selectPreview(series.poster_path)" >
                    <div class="info-text">
                        <h6>Titolo: {{series.name}}</h6>
                        <h6 v-if="series.name !== series.original_name"> Titolo originale: {{series.original_name}}</h6>
                        <h6>Lingua: <img :src="selectFlags(series.original_language)" alt=""></h6>
                        <h6>Voto: {{voteStarConv(series.vote_average)}}</h6>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Card",
    data(){
        return {
            voteStar: "ciao"
        }
    },
    props: {
        film: Array,
        series: Array,
        flags: Object
    },
    methods: {
        selectFlags(language) {
            if (!this.flags[language]) {
                return "https://images.emojiterra.com/twitter/v13.1/512px/1f30d.png"
            }
            return this.flags[language]
        },
        
        selectPreview(object){
            const urlImg = "https://image.tmdb.org/t/p/"
            const imgSize = "w342"

            if (!object) {
                return "https://geodis.com/us/sites/default/files/styles/max_800x800/public/2018-06/404.png?itok=NadF3Pmp"
            }

            return urlImg + imgSize + object
        },

        voteStarConv(number){
            // ricevo un voto da 1 a 10 con decimali
            // lo arrotondo per eccesso e divido per 2
            // mi ritornano 5 stelle, delle quali piene in base al numero che esce sopra
            
            
            
            const vote = Math.ceil(number / 2)
           
            return vote
        }
    }
}
</script>

<style lang="scss">
   .info-text{
       img{
           height: 20px;
       }
   }
</style>