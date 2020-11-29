<template>

  <v-container id="productInfo">
    
    <v-subheader>All Products</v-subheader>
    <v-divider></v-divider>
    <v-card class="mx-auto" outlined>
      <v-card-text>
        <v-row>
          <v-col cols="4" sm="4" md="3">
            <v-avatar size="100px" tile>
              <img
                alt="Avatar"
                src="https://res.cloudinary.com/sarbe/image/upload/v1605986250/diy/_detail_IMG_3695JPG_mpddha.jpg"
              />
            </v-avatar>
          </v-col>
          <v-col class="hidden-xs-only" sm="5" md="3">
            <strong></strong>
            <span class="grey--text"> Name:ABC Manufature:ABCD </span>
          </v-col>

          <v-col
            sm="3"
            md="6"
            class="grey--text text-truncate hidden-sm-and-down"
          >
             <v-btn color="primary" class="ma-2" dark @click="dialog = true">
        Open Dialog 1
      </v-btn>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </v-container>
</template>
<script>
export default {}
</script>
