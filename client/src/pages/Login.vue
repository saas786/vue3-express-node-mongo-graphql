<template>
  <div class="d-flex justify-content-center">
    <main class="box">
      <h2 class="mb-2">Login</h2>
      <div class="text-start text-danger my-2" v-if="error">{{ error }}</div>
      <form @submit.prevent="userLogin" novalidate>
        <div class="inputBox">
          <label for="email">Email</label>
          <input
            type="text"
            name="email"
            id="email"
            placeholder="Type your email"
            v-model="userData.email"
          />
        </div>
        <div class="inputBox">
          <label for="userPassword">Password</label>
          <input
            type="password"
            name="userPassword"
            id="userPassword"
            placeholder="Type your password"
            v-model="userData.password"
          />
        </div>
        <router-link class="forgot-password" to="/sendRequest"><p class="text-end  my-2">Forgot Password?</p></router-link>
        <div>
          <button type="submit" name="" style="float: left">Login</button>
          <router-link class="button" style="float: left" to="/register"
            >Register</router-link
          >
        </div>
      </form>
    </main>
  </div>
</template>

<script>
import { mapActions, mapState, mapMutations } from "vuex";

export default {
  name: "Login",
  data() {
    return {
      userData: {
        email: "",
        password: "",
      },
    };
  },
  computed: mapState("user", ["error"]),
  beforeUnmount() {
    this.$store.commit('user/setError','');
  },
  methods: {
    ...mapActions("user", ["login"]),
    ...mapMutations("user", ["setError"]),
    userLogin() {
      this.login(this.userData);
    },
  },
};
</script>

<style scoped>
.box {
  background-color: rgba(0, 0, 0, 0.8);
  border-radius: 10px;
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.8);
  margin-top: 80px;
  padding: 40px;
  /* position: absolute;
  top: 50%;
  left: 50%; */
  /* transform: translate(-50%, -50%); */
  text-align: left;
  width: 50vw;
  min-width: 350px;
}

.box h2 {
  margin: 0 0 30px 0;
  padding: 0;
  color: #fff;
  text-align: center;
}

.box .inputBox label {
  color: #fff;
}

.box .inputBox input {
  background: transparent;
  border: none;
  border-bottom: 1px solid #fff;
  color: #fff;
  font-size: 18px;
  letter-spacing: 2px;
  margin-bottom: 30px;
  outline: none;
  padding: 10px 0;
  width: 100%;
}

.box input[type="submit"],
.box button[type="submit"],
a.button {
  font-family: sans-serif;
  background: #03a9f4;
  /* font-size: 11px; */
  border: none;
  border-radius: 5px;
  color: #fff;
  cursor: pointer;
  /* font-weight: 600; */
  padding: 10px 20px;
  letter-spacing: 2px;
  outline: none;
  /* text-transform: uppercase; */
  text-decoration: none;
  margin: 2px 10px 2px 0;
  display: inline-block;
}

.box input[type="submit"]:hover,
.box button[type="submit"]:hover,
a.button:hover {
  opacity: 0.8;
}

.forgot-password {
  color: white;
}
.forgot-password:hover {
  color: lightgray;
  cursor: pointer;
  text-decoration: underline white;
}
</style>
