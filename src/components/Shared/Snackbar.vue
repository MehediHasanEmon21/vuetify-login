<template>
  <v-snackbar
      v-model="snackbar"
      top
      color="green"
    >
    {{snackbarText}}
    </v-snackbar>
</template>

<script>
export default {
    props:["snackbar","snackbarText"],
}
</script>

<style>

</style>