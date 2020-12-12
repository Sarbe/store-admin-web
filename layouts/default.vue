<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
      light
      permanent
      style="box-shadow: 0 0 8px 0 rgba(0, 0, 0, 0.2)"
    >
      <!-- Profile section -->
      <v-list>
        <v-list-item>
          <v-list-item-avatar>
            <v-img src="https://cdn.vuetifyjs.com/images/john.png"></v-img>
          </v-list-item-avatar>
        </v-list-item>

        <v-list-item link>
          <v-list-item-content>
            <v-list-item-title class="title"> Sarbeswar </v-list-item-title>
            <v-list-item-subtitle>sarbe@ss.com</v-list-item-subtitle>
          </v-list-item-content>

          <v-list-item-action>
            <v-icon>mdi-menu-down</v-icon>
          </v-list-item-action>
        </v-list-item>
      </v-list>
      <v-divider></v-divider>
      <!-- Menu -->

      <v-list nav>
        <v-list-group
          v-for="item in items"
          :key="item.title"
          :prepend-icon="item.action"
          no-action
        >
          <template v-slot:activator>
            <v-list-item-content>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item-content>
          </template>

          <v-list-item
            v-for="(subItem, j) in item.subItems"
            :key="j"
            :to="subItem.to"
            router
            exact
          >
            <!-- <v-list-item-action>
              <v-icon>{{ child.icon }}</v-icon>
            </v-list-item-action> -->
            <v-list-item-content>
              <v-list-item-title v-text="subItem.title" />
            </v-list-item-content>
          </v-list-item>
        </v-list-group>
      </v-list>
      <!-- drawer -->
    </v-navigation-drawer>

    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>mdi-minus</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" />
      <!-- <v-spacer />
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
      /> -->
      <v-spacer />
      <v-btn icon>
        <v-icon color="green darken-2"> mdi-domain </v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon color="blue darken-2"> mdi-message-text </v-icon>
      </v-btn>
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-avatar>
            <img
              v-bind="attrs"
              v-on="on"
              src="https://cdn.vuetifyjs.com/images/john.jpg"
              alt="John"
            />
          </v-avatar>
        </template>
        <span>User</span>
      </v-tooltip>
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main id="main-body">
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light> mdi-repeat </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <!--  :absolute="!fixed"-->
    <v-footer app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
       clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          action: 'mdi-ticket',
          subItems: [
            { title: 'List Products', to: '/products' },
            { title: 'Add Product', to: '/products' },
          ],
          title: 'Products',
        },
        {
          action: 'mdi-silverware-fork-knife',
          active: true,
          subItems: [{ title: 'List Users', to: '/users' }],
          title: 'Users',
        },
        {
          action: 'mdi-silverware-fork-knife',
          active: true,
          subItems: [{ title: 'Roles', to: '/roles' }],
          title: 'Configuration',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'DiyComponents',
    }
  },
}
</script>
<style scoped>
a {
  color: black !important;
}
.list-item--active .v-list-item__title {
  color: black !important;
}
#main-body {
  background-color: #f2f5f8;
}
</style>
