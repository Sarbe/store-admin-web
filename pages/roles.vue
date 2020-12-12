<template>
  <v-container>
    <v-tabs v-model="tab">
      <v-tab>Entitlements</v-tab>
      <v-tab>Roles</v-tab>
      <v-tab>Policy</v-tab>
    </v-tabs>
    <v-tabs-items v-model="tab">
      <v-tab-item>
        <v-card flat>
          <v-card-text>
            <v-treeview :items="entitlements"></v-treeview>
          </v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card flat>
          <v-card-text> </v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card flat>
          <v-card-text>
            <v-container>
              <!-- <v-select
                v-model="selectionType"
                :items="['leaf', 'independent']"
                label="Selection type"
              ></v-select> -->
              <v-row>
                <v-col>
                  <v-treeview
                    v-model="selection"
                    :items="entitlements"
                    selection-type="leaf"
                    selectable
                    return-object
                    open-all
                  ></v-treeview>
                </v-col>
                <v-divider vertical></v-divider>
                <v-col class="pa-6" cols="6">
                  <template v-if="!selection.length">
                    No nodes selected.
                  </template>
                  <template v-else>
                    <div v-for="node in selection" :key="node.name">
                      {{ node.name }}
                    </div>
                  </template>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      show: false,
      tab: null,
      selection: [],
      entitlements: [
        {
          id: 1,
          name: 'users',
          children: [
            { id: 11, name: 'List User', value: 'listUsers' },
            { id: 12, name: 'View User', value: 'viewUsers' },
            { id: 13, name: 'Edit User', value: 'editUser' },
            { id: 14, name: 'Add User', value: 'addUser' },
            { id: 15, name: 'Delete User', value: 'deleteUser' },
            { id: 16, name: 'Export User', value: 'exportUser' },
          ],
        },
        {
          id: 2,
          name: 'products',
          children: [
            { id: 21, name: 'List Products', value: 'listProducts' },
            { id: 22, name: 'View Products', value: 'viewProducts' },
            { id: 23, name: 'Edit Products', value: 'editProduct' },
            { id: 24, name: 'Add Products', value: 'addProduct' },
            {
              id: 25,
              name: 'Delete Products',
              value: 'deleteProduct',
              group: 'Products',
            },
          ],
        },
        {
          id: 3,
          name: 'Account',
          children: [],
        },
        {
          id: 4,
          name: 'Config',
          children: [
            {
              id: 41,
              name: 'Roles',
              value: 'roles',
              children: [
                { id: 411, name: 'List Roles', value: 'listRoles' },
                { id: 412, name: 'View Roles', value: 'viewRoles' },
                { id: 413, name: 'Create Role', value: 'createRole' },
                { id: 414, name: 'Edit Role', value: 'editRole' },
                { id: 415, name: 'Delete Roles', value: 'deleteRole' },
              ],
            },
            {
              id: 42,
              name: 'Entitlements',
              value: 'entitlements',
              children: [
                {
                  id: 421,
                  name: 'List Entitlements',
                  value: 'viewEntitlements',
                },
                {
                  id: 422,
                  name: 'View Entitlements',
                  value: 'viewEntitlement',
                },
                {
                  id: 423,
                  name: 'Cretae Entitlements',
                  value: 'createEntitlement',
                },
                {
                  id: 424,
                  name: 'Edit Entitlements',
                  value: 'editEntitlement',
                },
                {
                  id: 425,
                  name: 'Delete Entitlements',
                  value: 'deleteEntitlement',
                },
              ],
            },
            {
              id: 43,
              name: 'Policy',
              value: 'policy',
              children: [
                { id: 431, name: 'List Mappings', value: 'listMappings' },
                { id: 432, name: 'View Mapping', value: 'viewMapping' },
                { id: 433, name: 'Create Mapping', value: 'createMapping' },
                { id: 434, name: 'Edit Mapping', value: 'editMapping' },
                { id: 435, name: 'Delete Mapping', value: 'deleteMapping' },
              ],
            },
          ],
        },
      ],
      roles: [
        {
          roleName: 'Administrator',
          desc: 'Administrator User',
          entitlements: [
            { name: 'List User', value: 'listUsers', group: 'Users' },
            { name: 'View User', value: 'viewUsers', group: 'Users' },
            { name: 'Edit User', value: 'editUser', group: 'Users' },
            { name: 'Add User', value: 'addUser', group: 'Users' },
            { name: 'Delete User', value: 'deleteUser', group: 'Users' },
            { name: 'Export User', value: 'exportUser', group: 'Users' },
            { name: 'List Products', value: 'listProducts', group: 'Products' },
            { name: 'View Products', value: 'viewProducts', group: 'Products' },
            { name: 'Edit Products', value: 'editProduct', group: 'Products' },
            { name: 'Add Products', value: 'addProduct', group: 'Products' },
            {
              name: 'Delete Products',
              value: 'deleteProduct',
              group: 'Products',
            },
          ],
        },
        {
          roleName: 'EndUser',
          desc: 'End Customer',
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
          desc: 'Suppport Esecutive',
          entitlements: [
            { name: 'List User', value: 'users', group: 'Users' },
            { name: 'View User', value: 'users/?', group: 'Users' },
            { name: 'Edit User', value: 'users', group: 'Users' },
            { name: 'Export User', value: 'users', group: 'Users' },
            { name: 'List Products', value: 'products/all', group: 'Products' },
            {
              name: 'View Products',
              value: 'products/edit/?',
              group: 'Products',
            },
            { name: 'Edit Products', value: 'products', group: 'Products' },
            { name: 'Add Products', value: 'products', group: 'Products' },
          ],
        },
      ],
      files: [
        {
          color: 'blue',
          icon: 'mdi-clipboard-text',
          subtitle: 'Jan 20, 2014',
          title: 'Vacation itinerary',
        },
        {
          color: 'amber',
          icon: 'mdi-gesture-tap-button',
          subtitle: 'Jan 10, 2014',
          title: 'Kitchen remodel',
        },
      ],
      folders: [
        {
          subtitle: 'Jan 9, 2014',
          title: 'Photos',
        },
        {
          subtitle: 'Jan 17, 2014',
          title: 'Recipes',
        },
        {
          subtitle: 'Jan 28, 2014',
          title: 'Work',
        },
      ],
    }
  },
  computed: {
    getRoleGroup() {
      var unique
      var c = []
      this.entitlements.forEach((val) => {
        c.push(val.group)
      })
      unique = c.filter((v, i, a) => a.indexOf(v) === i)
      console.log(unique)
      return unique
    },
  },
}
</script>

<style scoped></style>
