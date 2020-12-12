<template>
  <v-card class="ma-1 pa-1 prdCard" width="200px">
    <nuxt-link :to="`/details`">
      <v-img
        class="pa-1"
        height="130px"
        src="https://cdn.britannica.com/77/170477-050-1C747EE3/Laptop-computer.jpg"
      ></v-img>
    </nuxt-link>
    <v-card-text class="ma-1 pa-0">
      <h4 class="text-md-body-1 ma-2 pa-0" style="color: green">
        &#8377; <b>1200</b>
      </h4>
      <nuxt-link :to="`details`">
        <p class="text-md-body-2 text-decoration-none blue--text">
          Top western road trips
        </p>
      </nuxt-link>
    </v-card-text>

    <v-rating
      v-model="rating"
      background-color="orange lighten-3"
      color="orange"
      small
      readonly
      dense
      class="d-inline"
    ></v-rating>
    <h5 class="d-inline ml-2 caption">{{ rating }}</h5>
    <div>
      <v-progress-linear
        class="my-2"
        height="10"
        v-model="progress"
        color="amber"
      ></v-progress-linear>
      <h4 class="caption">Sold: {{ valueDeterminate }}</h4>
    </div>
  </v-card>
</template>
<script>
export default {
  props: {
    cardType: String,
  },
  data() {
    return {
      rating: 2,
      progress: 30,
      valueDeterminate: 20,
    }
  },
}
</script>
<style scoped>
.prdCard {
  box-shadow: none !important;
  width: 195px;
}
.prdCard * {
  font-family: 'Work Sans', sans-serif !important;
}
</style>
