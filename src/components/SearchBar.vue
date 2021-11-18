<template>
  <div>
      <input type="text" @keydown.enter="textEmit" v-model="textSearch">
  </div>
</template>

<script>
export default {
    name: "SearchBar",
    data(){
        return {
            textSearch: ""
        }
    },
    methods: {
        textEmit() {
            this.$emit("textSearch", this.textSearch)
        }
    }
}
</script>

<style>

</style>