<template>
  <v-container mt-5>
    <vue-element-loading
      is-full-screen
      :active="showCustomizeLoader"
      background-color="rgba(100, 100, 100, 0.4)"
    >
      <img
        src="https://firebasestorage.googleapis.com/v0/b/csgo-auction.appspot.com/o/side-03.png?alt=media&token=91ce7293-e061-4a46-8929-d72bb6917499"
        class="my-3 rotate-vert-center"
        height="250px"
      />
    </vue-element-loading>
    <v-card pa-2 width="90%" class="mx-auto">
      <v-row>
        <v-col cols="12" md="5" xs="12" justify="center" align="center">
          <img
            width="50%"
            src="https://firebasestorage.googleapis.com/v0/b/csgo-auction.appspot.com/o/side-03.png?alt=media&token=91ce7293-e061-4a46-8929-d72bb6917499"
          />
        </v-col>
        <v-col cols="12" md="7" xs="12" justify="center" align="center" class="mt-5">
          <h1 class="fin">{{ data.tag}}</h1>
          <v-card-text>
            <p class="lexend" style="font-size: 25px">{{ data.name}}</p>
            <p class="size lexend">Primary Weapon: {{ data.primary_weapon}}</p>
            <p class="size lexend">Secondary Weapon: {{ data.secondary_weapon}}</p>
            <p class="size lexend">Category: To be decided</p>
            <p class="size lexend">Team: To be Auctioned</p>
            <h2>{{ data.category}}</h2>
          </v-card-text>
        </v-col>
      </v-row>
    </v-card>
  </v-container>
</template>
<script>
const fb = require("../firebaseConfig");
import VueElementLoading from "vue-element-loading";

export default {
  name: "profile",
  props: ["id"],
  data() {
    return {
      data: {},
      showCustomizeLoader: true
    };
  },
  components: {
    VueElementLoading
  },
  created() {
    setTimeout(() => {
      this.showCustomizeLoader = false;
    }, 2000);
    fb.playersCollection
      .doc(this.$route.params.id)
      .get()
      .then(res => {
        this.data = res.data();
      });
  }
};
</script>