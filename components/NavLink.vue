<template>
  <v-breadcrumbs :items="links">
    <template v-slot:divider>
      <v-icon>mdi-chevron-right</v-icon>
    </template>
  </v-breadcrumbs>
</template>

<script>
export default {
  props: { links: Array },
}
</script>

<style scoped>
ul.v-breadcrumbs {
  padding-left: 0px !important;
}
a.v-breadcrumbs__item {
  font-size: 20px !important;
}
</style>
