<template>
  <v-app>

    <div class="backgruond"></div>

    <v-main class="d-flex justify-center align-center">

      <v-col cols="10" lg="4" class="mx-auto">

        <v-card class="pa-4">
          <div class="text-center">
            <v-avatar size="100" color="indigo lighten-4">
              <v-icon size="60" color="indigo">mdi-account</v-icon>
            </v-avatar>
            <h2 class="pt-3 indigo--text">Login Form</h2>
          </div>

          <v-form ref="form" @submit.prevent="submitForm">
              <v-card-text>
                <v-text-field
                  label="Email"
                  type="text"
                  prepend-inner-icon="mdi-account"
                  v-model="form.email"
                  :rules="emailRules"
                >
                </v-text-field>
                <v-text-field
                  label="Password"
                  :type="showPassword ? 'text' : 'password'"
                  prepend-inner-icon="mdi-key"
                  :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                  @click:append="showPassword = !showPassword"
                  v-model="form.password"
                  :rules="passwordRules"
                >
                </v-text-field>
                <v-switch lable="remember me"></v-switch>
              </v-card-text>

              <v-card-actions class="justify-center">
                <v-btn :loading="loading" type="submit" color="indigo" class="white--text px-8">Login</v-btn>
              </v-card-actions>
          </v-form>
        
        </v-card>

      </v-col>
     
    </v-main>
   <Snackbar :snackbar="snackbar" :snackbarText="snackbarText"></Snackbar>
  </v-app>
</template>

<script>


import Snackbar from './components/Shared/Snackbar.vue';
export default {
  name: 'App',
  data: () => ({
    showPassword: false,
    loading: false,
    form: {
      email: '',
      password: '',
    },
    snackbar: false,
    snackbarText: "Successfully Login",
    emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid',
    ],
    passwordRules: [
        v => !!v || 'Password is required',
        v => v.length >= 6 || 'Password must be greater than 6 characters',
    ],
  }),
  components:{
    Snackbar
  },
  methods: {
    submitForm(){
      if(this.$refs.form.validate()){
        this.loading = true;
        setTimeout(()=> {
          this.loading = false;
          this.snackbar = true;
          this.$refs.form.reset()
          },3000)
      }
    }
  }
};
</script>

<style scoped>
.backgruond{
    background-image: url(./assets/Order-Banner.jpg) !important;
    height: 300px;
    width: 100%;
    display: block;
    position: absolute;
    top: 0;
    background-size: cover;
  }
</style>
