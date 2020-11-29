<template>
  <v-container>
    <!-- <div style="text-align: center">
      <v-avatar size="100">
        <img src="https://cdn.vuetifyjs.com/images/john.jpg" alt="John" />
      </v-avatar>
    </div> -->
    <NavLink :links="navlinks"/>

    <h3>User: {{userDetails.firstName}}</h3>
    <p class="text-subtitle-1">ID: {{ userDetails.id }}</p>
    <p class="text-subtitle-1">Role: {{ userDetails.role }}</p>

    <v-tabs v-model="tab" background-color="#f2f5f8">
      <v-tab>Profile</v-tab>
      <v-tab>Orders</v-tab>
      <v-tab>Others</v-tab>
    </v-tabs>

    <v-tabs-items v-model="tab">
      <!-- Profile -->

      <v-tab-item class="pt-6" style="background-color: #f2f5f8">
        <v-card
          color="amber darken-1"
          light
          class="pa-2"
          v-if="!userDetails.enabled"
        >
          <v-card-title class="headline"> User is Disabled </v-card-title>

          <v-card-subtitle>
            User is currently disabled. Login Access has been revoked.
          </v-card-subtitle>

          <v-card-actions>
            <v-btn dark @click="enableUser(userDetails.id)">
              <v-icon class="mr-2">mdi-account-check</v-icon>
              Enable User
            </v-btn>
          </v-card-actions>
        </v-card>
        <!-- Basic Information -->

        <v-expansion-panels accordion>
          <v-expansion-panel class="mt-4" style="border-radius: 5px">
            <v-expansion-panel-header>
              <p class="text-h6">Basic Information</p>
            </v-expansion-panel-header>
            <v-expansion-panel-content>
              <v-row>
                <v-col cols="12" md="3" xs="12" class="text-center">
                  <v-avatar size="200">
                    <img
                      :src="userDetails.avatar"
                      :alt="userDetails.firstName"
                    />
                  </v-avatar>
                  <v-btn class="mt-4">Edit Photo</v-btn>
                </v-col>
                <v-col cols="12" md="9" xs="12">
                  <v-form ref="form" v-model="valid" lazy-validation>
                    <v-row>
                      <v-col cols="12" md="6">
                        <v-text-field
                          v-model="userDetails.firstName"
                          :counter="10"
                          :rules="nameRules"
                          label="First Name"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" md="6">
                        <v-text-field
                          v-model="userDetails.lastName"
                          :counter="10"
                          :rules="nameRules"
                          label="Last Name"
                          required
                        ></v-text-field>
                      </v-col>
                      <!-- <v-col cols="12">
                        Gender:
                        <v-radio-group v-model="row" row>
                          <v-radio label="MALE" value="MALE"></v-radio>
                          <v-radio label="FEMALE" value="FEMALE"></v-radio>
                        </v-radio-group>
                      </v-col> -->
                      <v-col cols="12" md="6" xs="10">
                        <v-text-field
                          v-model="userDetails.phoneNbr"
                          :counter="10"
                          :rules="nameRules"
                          label="Phone"
                          required
                          type="phone"
                          maxlength="10"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" md="6">
                        <p v-if="!userDetails.enabled">
                          <v-icon color="green">mdi-check-decagram</v-icon>
                          Verifed
                        </p>
                        <v-btn v-else> Verfiy Number </v-btn>
                      </v-col>

                      <v-col cols="12" md="6">
                        <v-text-field
                          v-model="userDetails.email"
                          :counter="10"
                          :rules="emailRules"
                          label="Email"
                          required
                          type="email"
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12" md="6">
                        <p v-if="userDetails.enabled">
                          <v-icon color="green">mdi-check-decagram</v-icon>
                          Verifed
                        </p>
                        <v-btn v-else> Send Verification Mail </v-btn>
                      </v-col>

                      <v-col cols="12">
                        <v-btn
                          color="cyan"
                          class="mr-4"
                          @click="saveUserDetails"
                        >
                          Save
                        </v-btn>
                      </v-col>
                    </v-row>
                  </v-form>
                </v-col>
              </v-row>
            </v-expansion-panel-content>
          </v-expansion-panel>
          <v-expansion-panel class="mt-4">
            <v-expansion-panel-header>
              <p class="text-h6">Address</p>
            </v-expansion-panel-header>
            <v-expansion-panel-content>
              <v-card
                class="mx-auto mb-1"
                v-for="add in userDetails.address"
                :key="add.name"
                elevation="0"
                outlined
              >
                <v-card-title>
                  <div class="overline mb-2 blue-grey lighten-5 px-2">
                    {{ add.type }}
                  </div>

                  <v-spacer></v-spacer>
                  <v-menu bottom open-on-hover offset-y>
                    <template v-slot:activator="{ on, attrs }">
                      <v-btn dark icon v-bind="attrs" v-on="on">
                        <v-icon color="black">mdi-dots-vertical</v-icon>
                      </v-btn>
                    </template>

                    <v-list>
                      <v-list-item link>
                        <v-list-item-title>Edit</v-list-item-title>
                      </v-list-item>
                      <v-list-item link>
                        <v-list-item-title>Delete</v-list-item-title>
                      </v-list-item>
                    </v-list>
                  </v-menu>
                </v-card-title>
                <v-card-text>
                  <span class="d-block text-subtitle-2">
                    {{ add.name }}&nbsp;&nbsp;&nbsp;{{ add.phone }}
                  </span>
                  {{ add.line }}, {{ add.city }}, {{ add.state }} -
                  <b>{{ add.pincode }}</b>
                </v-card-text>
              </v-card>
            </v-expansion-panel-content>
          </v-expansion-panel>
          <v-expansion-panel class="mt-4">
            <v-expansion-panel-header>
              <p class="text-h6">Action</p>
            </v-expansion-panel-header>
            <v-expansion-panel-content>
              <v-card elevation="0" class="mb-6">
                <v-card-title class="headline">
                  Reset User Password
                </v-card-title>
                <v-card-subtitle>
                  Sends a password reset mail to user's mail address
                </v-card-subtitle>

                <v-card-actions>
                  <v-btn color="white" elevation="10">
                    <v-icon left> mdi-email-send </v-icon>
                    Send Password Reset Mail
                  </v-btn>
                </v-card-actions>
              </v-card>
              <v-divider></v-divider>
              <v-card elevation="0" class="mb-6">
                <v-card-title class="headline"> Export User Data </v-card-title>

                <v-card-subtitle> Exports user data </v-card-subtitle>

                <v-card-actions>
                  <v-btn color="cyan" elevation="10">
                    <v-icon left> mdi-application-export </v-icon>
                    Export Data
                  </v-btn>
                </v-card-actions>
              </v-card>
              <v-divider></v-divider>
              <v-card elevation="0" class="mb-4">
                <v-card-title class="headline"> Delete User </v-card-title>

                <v-card-subtitle> Delete User Details </v-card-subtitle>

                <v-card-actions>
                  <v-btn color="error" elevation="10">
                    <v-icon left> mdi-delete </v-icon>
                    Delete User
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-expansion-panel-content>
          </v-expansion-panel>
          <v-expansion-panel class="mt-4">
            <v-expansion-panel-header>
              <p class="text-h6">Raw Data</p>
            </v-expansion-panel-header>
            <v-expansion-panel-content> </v-expansion-panel-content
          ></v-expansion-panel>
        </v-expansion-panels>
      </v-tab-item>
      <!-- Order Details -->
      <v-tab-item>
        <v-container>
          <v-card>
            <v-card-title>
              Nutrition
              <v-spacer></v-spacer>
              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Search"
                single-line
                hide-details
              ></v-text-field>
            </v-card-title>
            <v-data-table
              :headers="headers"
              :items="orders"
              :search="search"
            ></v-data-table>
          </v-card>
        </v-container>
      </v-tab-item>
    </v-tabs-items>
  </v-container>
</template>

<script>
import NavLink from '@/components/NavLink'
export default {
  components: [NavLink],
  data() {
    return {
      navlinks: [
        {
          text: 'Dashboard',
          disabled: false,
          href: 'breadcrumbs_dashboard',
        },
        {
          text: 'Users',
          disabled: false,
          href: 'breadcrumbs_link_1',
        },
        {
          text: 'name',
          disabled: true,
          href: 'breadcrumbs_link_2',
        },
      ],
      tab: null,
      search: '',
      userDetails: {
        id: '10',
        email: 'abc@abc.com',
        firstName: 'Sarbeswar',
        lastName: 'Sethi',
        enabled: false,
        created: '2019-08-09T03:14:12Z',
        lastSignIn: '2019-08-14T20:00:53Z',
        role: 'ADMIN',
        phoneNbr: 9776993796,
        avatar: 'https://cdn.vuetifyjs.com/images/john.jpg',
        address: [
          {
            type: 'HOME',
            name: 'Abc',
            phone: '9776998899',
            pincode: 756567,
            locality: 'patis',
            line: 'Qr No- B/1686,Naloc Nagar',
            city: 'Bhubaneswar',
            state: 'Odisha',
            landmark: '',
            alternatePhone: '',
          },
          {
            type: 'HOME',
            name: 'Sarbeswar Sethi',
            phone: '9776998899',
            pincode: 756567,
            locality: 'patis',
            line: 'Qr No- B/1686,Naloc Nagar',
            city: 'Bhubaneswar',
            state: 'Odisha',
            landmark: '',
            alternatePhone: '',
          },
          {
            type: 'OFFICE',
            name: 'Sujata Dung Dung',
            phone: '9776998899',
            pincode: 756567,
            locality: 'patis',
            line: 'Qr No- B/1686,Naloc Nagar',
            city: 'Bhubaneswar',
            state: 'Odisha',
            landmark: '',
            alternatePhone: '',
          },
        ],
      },

      headers: [
        { text: 'Order ID', value: 'orderId' },
        { text: 'Order Name', value: 'orderName' },
        { text: 'Actions', value: 'actions', sortable: false },
      ],
      orders: [
        { orderId: 1, orderName: 'Order1' },
        { orderId: 2, orderName: 'Order2' },
        { orderId: 3, orderName: 'Order3' },
      ],
    }
  },
  computed: {
    getTabKeys() {
      return Object.keys(this.userDetails)
    },
  },
  methods: {
    enableUser(id) {
      //Call API
      this.userDetails.enabled = true
    },
    getOrders() {
      sleep(5000)
      return this.orders
    },
  },
}
</script>

<style></style>
