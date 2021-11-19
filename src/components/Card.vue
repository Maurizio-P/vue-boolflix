<template>
  <div class="row">
    <section class="film">
      <h2>Film</h2>
      <div class="container-row">
        <div class="my-row">
          <div class="my-card" v-for="movie in film" :key="movie.id">
            <img class="poster" :src="selectPreview(movie.poster_path)" />
            <div class="info-text">
              <h6>Titolo: {{ movie.title }}</h6>
              <h6 v-if="movie.title !== movie.original_title">
                Titolo originale: {{ movie.original_title }}
              </h6>
              <h6>
                Lingua:
                <img :src="selectFlags(movie.original_language)" alt="" />
              </h6>
              <h6>
                Voto:
                <i
                  v-for="(star, i) in 5"
                  :key="i"
                  class="fas fa-star"
                  :class="Math.ceil(movie.vote_average / 2) > i ? '' : 'd-none'"
                ></i>
                <i
                  v-for="(star, y) in 5"
                  :key="y"
                  class="far fa-star"
                  :class="
                    Math.ceil(movie.vote_average / 2) < y + 1 ? '' : 'd-none'
                  "
                ></i>
              </h6>
              <div class="overview-container">
                <div class="overview">
                  {{ movie.overview }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="series">
      <h2>Serie</h2>
      <div class="container-row">
      <div class="my-row">
        <div class="my-card" v-for="series in series" :key="series.id">
          <img class="poster" :src="selectPreview(series.poster_path)" />
          <div class="info-text">
            <h6>Titolo: {{ series.name }}</h6>
            <h6 v-if="series.name !== series.original_name">
              Titolo originale: {{ series.original_name }}
            </h6>
            <h6>
              Lingua:
              <img :src="selectFlags(series.original_language)" alt="" />
            </h6>
            <h6>
              Voto:
              <i
                v-for="(star, i) in 5"
                :key="i"
                class="fas fa-star"
                :class="Math.ceil(series.vote_average / 2) > i ? '' : 'd-none'"
              ></i>
              <i
                v-for="(star, i) in 5"
                :key="i"
                class="far fa-star"
                :class="
                  Math.ceil(series.vote_average / 2) < i + 1 ? '' : 'd-none'
                "
              ></i>
            </h6>
            <div class="overview-container">
              <div class="overview">
                {{ series.overview }}
              </div>
            </div>
          </div>
        </div>
      </div>

      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
      classStar: "fas fa-star",
    };
  },
  props: {
    film: Array,
    series: Array,
    flags: Object,
  },
  methods: {
    selectFlags(language) {
      if (!this.flags[language]) {
        return "https://images.emojiterra.com/twitter/v13.1/512px/1f30d.png";
      }
      return this.flags[language];
    },

    selectPreview(object) {
      const urlImg = "https://image.tmdb.org/t/p/";
      const imgSize = "w342";

      if (!object) {
        return "https://geodis.com/us/sites/default/files/styles/max_800x800/public/2018-06/404.png?itok=NadF3Pmp";
      }

      return urlImg + imgSize + object;
    },

    // voteConv(number){
    //     const vote = Math.ceil(number / 2)
    //     return vote
    // },
  },
};
</script>

<style lang="scss">
.row {
  display: flex;
  flex-direction: column;

  section {
    padding: 15px 25px;

    h2{
        color: white;
    }
    .container-row {
        overflow: auto;
      .my-row {
        display: flex;
        height: 550px;


        .my-card {
          position: relative;
          width: 342px;
          height: 513px;
          flex-shrink: 0;
          flex-grow: 0;
          margin-right: 20px;
          transition: .5s;
          &:hover {
            transform: scale(1.1);
            .info-text {
              opacity: 1;
            }
          }
          .poster {
            width: 100%;
            height: 100%;
          }
        }
        .info-text {
          position: absolute;
          top: 0;
          left: 0;
          right: 0;
          bottom: 0;
          background-color: rgba($color: #000000, $alpha: 0.5);
          color: white;
          opacity: 0;
          display: flex;
          flex-direction: column;
          justify-content: center;
          align-items: center;
          padding: 10px;
          backdrop-filter: blur(2px);

          img {
            height: 20px;
          }

          .overview-container {
            overflow: auto;
            max-height: 270px;
          }
        }
      }
    }
  }
}
</style>