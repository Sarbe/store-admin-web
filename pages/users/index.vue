<template>
  <v-container>
    <v-data-table
      :headers="headers"
      :items="users"
      sort-by="firstName"
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>My CRUD</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
        </v-toolbar>
      </template>
      <template v-slot:item.actions="{ item }">
        <v-btn text to="/users/1">
          <v-icon small> mdi-pencil </v-icon>
        </v-btn>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize">Reset</v-btn>
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    users: [
      {
        id: '10',
        email: 'sasmit.hota@abc.com',
        firstName: 'Sasmit',
        lastName: 'Hota',
        enabled: false,
        created: '2019-08-09T03:14:12Z',
        lastSignIn: '2019-08-14T20:00:53Z',
        role: 'ADMIN',
        phoneNbr: 9776993796,
        avatar: 'https://cdn.vuetifyjs.com/images/john.jpg',
      },
      {
        id: '11',
        email: 'abc@abc.com',
        firstName: 'Sarbeswar',
        lastName: 'Sethi',
        enabled: false,
        created: '2019-08-09T03:14:12Z',
        lastSignIn: '2019-08-14T20:00:53Z',
        role: 'ADMIN',
        phoneNbr: 9776993796,
        avatar: 'https://cdn.vuetifyjs.com/images/john.jpg',
      },
      {
        id: '12',
        email: 'abc@abc.com',
        firstName: 'Priyanshu',
        lastName: 'Sethi',
        enabled: false,
        created: '2019-08-09T03:14:12Z',
        lastSignIn: '2019-08-14T20:00:53Z',
        role: 'USER',
        phoneNbr: 9776993796,
        avatar: 'https://cdn.vuetifyjs.com/images/john.jpg',
      },
      {
        id: '13',
        email: 'abc@abc.com',
        firstName: 'Abhisekh',
        lastName: 'Shah',
        enabled: false,
        created: '2019-08-09T03:14:12Z',
        lastSignIn: '2019-08-14T20:00:53Z',
        role: 'USER',
        phoneNbr: 9776993796,
        avatar: 'https://cdn.vuetifyjs.com/images/john.jpg',
      },
    ],

    headers: [
      {
        text: 'First Name',
        align: 'start',
        sortable: false,
        value: 'firstName',
      },
      { text: 'Last Name', value: 'lastName' },
      { text: 'Email', value: 'email' },
      { text: 'Role', value: 'role' },
      { text: 'Phone Nbr', value: 'phoneNbr' },
      { text: 'Actions', value: 'actions', sortable: false },
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      name: '',
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0,
    },
    defaultItem: {
      name: '',
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0,
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
    },
  },

  watch: {
    dialog(val) {
      val || this.close()
    },
  },

  created() {
    this.initialize()
  },

  methods: {
    initialize() {
      this.desserts = [
        {
          name: 'Frozen Yogurt',
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
        },
        {
          name: 'Ice cream sandwich',
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
        },
        {
          name: 'Eclair',
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
        },
        {
          name: 'Cupcake',
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
        },
        {
          name: 'Gingerbread',
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
        },
        {
          name: 'Jelly bean',
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
        },
        {
          name: 'Lollipop',
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
        },
        {
          name: 'Honeycomb',
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
        },
        {
          name: 'Donut',
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
        },
        {
          name: 'KitKat',
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
        },
      ]
    },

    editItem(item) {
      this.$router.push({ path: 'users/1' })
    },

    deleteItem(item) {
      const index = this.desserts.indexOf(item)

      confirm('Are you sure you want to delete this item?') &&
        this.desserts.splice(index, 1)
    },

    close() {
      this.dialog = false
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      })
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem)
      } else {
        this.desserts.push(this.editedItem)
      }
      this.close()
    },
  },
}
</script>
