<template>
  <div>
      <ContainerCard />
  </div>
</template>

<script>
import ContainerCard from "./ContainerCard.vue"
export default {
    name: "Page",
    components: {
        ContainerCard
    }
    }
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap"
</style>