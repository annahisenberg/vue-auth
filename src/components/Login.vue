<template>
  <div>
    <b-form class="login" @submit.prevent="login">
      <h1>Sign in</h1>
      <b-form-group label="Email:" label-for="email">
        <b-form-input
          id="email"
          required
          v-model.trim="$v.email.$model"
          :state="$v.email.$dirty ? !$v.email.$error : null"
          type="email"
          placeholder="Enter email address"
        />
      </b-form-group>

      <b-form-group label="Password:" label-for="password">
        <b-form-input
          id="password"
          required
          v-model.trim="$v.password.$model"
          :state="$v.password.$dirty ? !$v.password.$error : null"
          type="password"
          placeholder="Password"
        />
      </b-form-group>
      <hr>

      <div v-if="authStatus != 'loading'">
        <b-button
          type="submit"
          variant="primary"
          :disabled="$v.email.$invalid || $v.password.$invalid"
        >Login</b-button>
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
      email: "",
      password: ""
    };
  },
  mixins: [validationMixin],
  validations: {
    email: {
      required
    },
    password: {
      required,
      minLength: minLength(3)
    }
  },
  computed: {
    authStatus() {
      return this.$store.getters.authStatus;
    }
  },
  methods: {
    login() {
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
