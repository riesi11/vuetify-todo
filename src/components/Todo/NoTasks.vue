<template>
  <div
      class="notasks"
  >
    <v-icon
        color="primary"
        size="100"
    >
      mdi-check
    </v-icon>
    <div class="text-h5 primary--text">No tasks</div>
  </div>

</template>

<script>
export default {

}
</script>

<style lang="sass">
.notasks
  position: absolute
  left: 50%
  top: 50%
  transform: translate(-50%, -50%)
  opacity: 50%
</style>