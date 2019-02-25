<template>
  <div>
    <b-form class="login" @submit.prevent="login">
      <h1>Sign in</h1>
      <b-form-group label="Email:" label-for="email">
        <b-form-input required v-model="username"/>
      </b-form-group>

      <b-form-group label="Password:" label-for="password">
        <b-form-input
          id="password"
          v-model.trim="$v.password.$model"
          :state="$v.password.$dirty ? !$v.password.$error : null"
          type="password"
          placeholder="Password"
        />
      </b-form-group>
      <hr>

      <div v-if="authStatus != 'loading'">
        <b-button type="submit" variant="primary" :disabled="$v.$invalid">Login</b-button>
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
import { validationMixin } from "vuelidate";
import { required, minLength } from "vuelidate/lib/validators";

export default {
  data() {
    return {
      username: "",
      password: ""
    };
  },
  mixins: [validationMixin],
  validations: {
    password: {
      required,
      minLength: minLength(7)
    }
  },
  computed: {
    authStatus() {
      return this.$store.getters.authStatus;
    }
  },
  methods: {
    login() {
      let v = this;
      let username = v.username;
      let password = v.password;
      this.$store
        .dispatch("login", { "username": v.username, "password": v.password })
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

.input.invalid input {
  border: 1px solid red;
  background: #ffc9aa;
}
</style>
