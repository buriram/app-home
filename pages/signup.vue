<template>
<v-parallax src="/pic/background.png" height="643">
          <v-card-media
          height="250"
          contain
          src="/pic/logo.png"
        >  
        </v-card-media>

    <v-card height="300" color="teal lighten-4">
    <form class="form-signin" @submit.prevent="login">
      <h2 class="form-signin-heading">Please sign up</h2>
      <input v-model="name" type="text" id="inputName" class="form-control" placeholder="Name" required autofocus>
      <input v-model="email" type="email" id="inputEmail" class="form-control" placeholder="Email address" required autofocus>
      <input v-model="password" type="password" id="inputPassword" class="form-control" placeholder="Password" required>
      <div class="text-xs-center">
        <v-btn color="orange" type="submit" >Sign up</v-btn>
      </div>
    </form>
    </v-card>

    <v-snackbar
      top
      v-model="snackbar"
    >
      login failed
      <v-btn flat color="pink" @click.native="snackbar = false">Close</v-btn>
    </v-snackbar>

  
</v-parallax>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      email: '',
      password: '',
      snackbar: false,
    }
  },
  methods: {
    async login () {
      let res = await this.$http.post('/auth',{email: this.email, password: this.password})
      if(res.data.ok){
        this.$router.push('/')
      } else{
        this.snackbar=true
      }
      //console.log(this.password)
    }
  }
}
</script>

<style lang="css">
body {
  background: #605B56;
}

.login-wrapper {
  background: #fff;
  width: 70%;
  margin: 12% auto;
}

.form-signin {
  max-width: 330px;
  padding: 10% 15px;
  margin: 0 auto;
}
.form-signin .form-signin-heading,
.form-signin .checkbox {
  margin-bottom: 10px;
}
.form-signin .checkbox {
  font-weight: normal;
}
.form-signin .form-control {
  position: relative;
  height: auto;
  -webkit-box-sizing: border-box;
          box-sizing: border-box;
  padding: 10px;
  font-size: 16px;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>