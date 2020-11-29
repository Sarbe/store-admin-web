<template>
  <v-container>
    <v-card elevation="0" class="mb-6">
      <v-card-title class="headline"> Available Roles </v-card-title>
      <v-card-subtitle> All roles </v-card-subtitle>
      <v-cart-text> </v-cart-text>
      <v-card-actions>
        <v-btn color="white" elevation="10">
          <v-icon left> mdi-email-send </v-icon>
          Add New Role
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      roles: [
        {
          roleName: 'Administrator',
          entitlements: [
            { name: 'List User', value: 'users', group: 'Users' },
            { name: 'View User', value: 'users/?', group: 'Users' },
            { name: 'Edit User', value: 'users', group: 'Users' },
            { name: 'Add User', value: 'users', group: 'Users' },
            { name: 'Delete User', value: 'users', group: 'Users' },
            { name: 'Export User', value: 'users', group: 'Users' },
            { name: 'List Products', value: 'products', group: 'Products' },
            { name: 'View Products', value: 'products', group: 'Products' },
            { name: 'Edit Products', value: 'products', group: 'Products' },
            { name: 'Add Products', value: 'products', group: 'Products' },
            { name: 'Delete Products', value: 'products', group: 'Products' },
          ],
        },
        {
          roleName: 'EndUser',
          entitlements: [
            { name: 'View User', value: 'users/?', group: 'Users' },
            { name: 'Edit User', value: 'users', group: 'Users' },
            { name: 'Delete User', value: 'users', group: 'Users' },
            { name: 'List Products', value: 'products', group: 'Products' },
            { name: 'View Products', value: 'products', group: 'Products' },
          ],
        },
        {
          roleName: 'Support',
          entitlements: [
            { name: 'List User', value: 'users', group: 'Users' },
            { name: 'View User', value: 'users/?', group: 'Users' },
            { name: 'Edit User', value: 'users', group: 'Users' },
            { name: 'Export User', value: 'users', group: 'Users' },
            { name: 'List Products', value: 'products/all', group: 'Products' },
            { name: 'View Products', value: 'products/edit/?', group: 'Products' },
            { name: 'Edit Products', value: 'products', group: 'Products' },
            { name: 'Add Products', value: 'products', group: 'Products' },
          ],
        },
      ],
    }
  },
}
</script>

<style scoped></style>
