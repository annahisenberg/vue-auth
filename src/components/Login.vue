<template>
  <div>
    <b-form class="login" @submit.prevent="login">
      <h1>Sign in</h1>
      <b-form-group label="Username:" label-for="username">
        <b-form-input required v-model="username"/>
      </b-form-group>

      <b-form-group label="Password:" label-for="password">
        <b-form-input
          id="password"
          type="password"
          v-model="password"
          placeholder="Password"
        />
      </b-form-group>
      <hr>

      <div v-if="authStatus != 'loading'">
        <b-button type="submit" variant="primary">Login</b-button>
      </div>

      <div v-if="authStatus === 'loading'">
        <b-button variant="primary" disabled>
          <b-spinner small type="grow"/>Loading...
        </b-button>
      </div>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: ""
    };
  },
  computed: {
    authStatus() {
      return this.$store.getters.authStatus;
    }
  },
  methods: {
    login() {
      let {username, password} = this;

      this.$store
        .dispatch("login", { username, password })
        .then(() => this.$router.push("/"))
        .catch(err => console.log(err));
    }
  }
};
</script>

<style scoped>
</style>
