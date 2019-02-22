<template>
  <div>
    <b-form class="login" @submit.prevent="login">
      <h1>Sign in</h1>
      <b-form-group label="Email:" label-for="email">
        <b-form-input
          id="email"
          required
          v-model="email"
          type="email"
          placeholder="Enter email address"
        />
      </b-form-group>

      <b-form-group label="Password:" label-for="password">
        <b-form-input
          id="password"
          required
          v-model="password"
          type="password"
          placeholder="Password"
        />
      </b-form-group>
      <hr>

      <b-button type="submit" variant="primary">Login</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    login: function() {
      let email = this.email;
      let password = this.password;
      this.$store
        .dispatch("login", { email, password })
        .then(() => this.$router.push("/"))
        .catch(err => console.log(err));
    }
  }
};
</script>

<style scoped>
input {
  width: 50%;
  margin: 0 auto;
}
</style>
