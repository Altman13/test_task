<template>
  <div class="home mt-5">
    <div class="alert alert-success" role="alert" v-if="success">
      {{ success }}
    </div>
    <div class="alert alert-danger" role="alert" v-if="error">
      {{ error }}
    </div>
    <h2 v-if="!user">Welcome, please log in or register</h2>
    <h2 v-else-if="!user.email_verified_at">
      Hello, {{ user.name }}! Principal Diagonal: {{ principal }} Secondary
      Diagonal: {{ secondary }}
    </h2>
    <h2 v-else>Hello, {{ user.name }}! You're in.</h2>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";

export default {
  name: "Home",

  data() {
    return {
      success: null,
      error: null,
      principal: null,
      secondary: null,
      mat: new Array(
        new Array(1, 2, 3, 4),
        new Array(5, 6, 7, 8),
        new Array(1, 2, 3, 4),
        new Array(5, 6, 7, 8)
      ),
    };
  },
  created: function () {
    this.printDiagonalSums()
  },
  computed: {
    ...mapGetters("auth", ["user"]),
  },

  methods: {
    ...mapActions("auth", ["sendVerifyResendRequest"]),
    printDiagonalSums() {
      for (var i = 0; i < this.mat.length; i++) {
        this.principal += this.mat[i][i];
        this.secondary += this.mat[i][this.mat.length - i - 1];
      }
      // console.log(`Principal Diagonal: ${principal}`);
      // console.log(`Secondary Diagonal: ${secondary}`);
    },
  },
};
</script>
