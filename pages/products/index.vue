<template>
  <v-container id="dashboard" fluid tag="section">
     <v-row>
          <v-col cols="12" md="3" sm="4" class="hidden-xs-only">
            Category
          </v-col>
            <v-col cols="12" md="9" sm="8" xs="12">
              Details
          </v-col>
    <!-- <ProductInfo v-for="i in 5" :key="i"/> -->
     </v-row>
  </v-container>
</template>

<script>
import ProductInfo  from '@/components/ProductInfo'
export default {
  components: { ProductInfo },
  data() {
    return {
      dialog: false,
      notifications: false,
      sound: true,
      widgets: false,
      items: ['Appetizers', 'Entrees', 'Deserts', 'Cocktails'],
      text:
        'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod ',
      selected: [2],
      items: [
        {
          action: '15 min',
          headline: 'Brunch this weekend?',
          subtitle: `I'll be in your neighborhood doing errands this weekend. Do you want to hang out?`,
          title: 'Ali Connors',
        },
        {
          action: '2 hr',
          headline: 'Summer BBQ',
          subtitle: `Wish I could come, but I'm out of town this weekend.`,
          title: 'me, Scrott, Jennifer',
        },
        {
          action: '6 hr',
          headline: 'Oui oui',
          subtitle: 'Do you have Paris recommendations? Have you ever been?',
          title: 'Sandra Adams',
        },
        {
          action: '12 hr',
          headline: 'Birthday gift',
          subtitle:
            'Have any ideas about what we should get Heidi for her birthday?',
          title: 'Trevor Hansen',
        },
        {
          action: '18hr',
          headline: 'Recipe to try',
          subtitle:
            'We should eat this: Grate, Squash, Corn, and tomatillo Tacos.',
          title: 'Britta Holt',
        },
      ],
    }
  },
  methods: {
    editProduct(prodId) {
      // fetch Product Full Data
      this.dialog = true
    },
  },
}
</script>
