<template>
  <v-container id="dashboard" fluid tag="section">
    <NavLink :links="navlinks" />

    <v-row>
      <v-col cols="12" md="3" sm="4" class="col-md-3 hidden-sm-and-down">
        <v-list dense class="grey lighten-4 pa-2">
          <v-subheader>CATEGORIES</v-subheader>
          <v-list-item link v-for="cat in categories" :key="cat">
            <v-list-item-content>
              <v-list-item-title> {{ cat }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-col>
      <v-col cols="12" md="9" sm="8" xs="12">
        <v-row>
          <v-col cols="12">
            <v-text-field
              flat
              solo-inverted
              rounded
              hide-details
              prepend-inner-icon="mdi-magnify"
              label="Search"
              align="center"
              justify="center"
              class="hidden-sm-and-down"
            />
          </v-col>
          <v-col cols="12" md="3" sm="12" xs="12" v-for="n in 10" :key="n">
            <ProductCardVertical />
          </v-col>
        </v-row>
      </v-col>
      <!-- <ProductInfo v-for="i in 5" :key="i"/> -->
    </v-row>
  </v-container>
</template>

<script>
import ProductInfo from '@/components/ProductInfo'
export default {
  components: { ProductInfo },
  data() {
    return {
      dialog: false,
      navlinks: [
        {
          text: 'Dashboard',
          disabled: false,
          href: 'breadcrumbs_dashboard',
        },
        {
          text: 'Products',
          disabled: false,
          href: 'breadcrumbs_link_1',
        },
        {
          text: 'name',
          disabled: true,
          href: 'breadcrumbs_link_2',
        },
      ],
       categories: [
        "All Categories",
        "Clothing & Apparel",
        "Garden & Kitchen",
        "Consumer Electrics",
        "Health & Beauty",
        "Computers & Technologies",
        "Jewelry & Watches",
        "Phones & Accessories",
        "Sport & Outdoor",
        "Babies & Moms",
      ],
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
