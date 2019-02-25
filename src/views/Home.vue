<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>Welcome Home, {{userInfo}}</h1>
  </div>
</template>

<script>
export default {
  name: "home",
  computed: {
    userInfo: function() {
      return this.$store.getters.userInfo;
    }
  }
};
</script>
