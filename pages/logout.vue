<template>
  <v-parallax src="/pic/background.png" height="643">
    <v-card-media
      height="250"
      contain
      src="/pic/logo.png"
    />
    <v-card height="250" color="teal lighten-4">
      <div class="text-xs-center">
        <v-btn color="warning" @click="Dologout">Sign Out.</v-btn>
      </div>
    </v-card>

  </v-parallax>
</template>
<script>
export default {
  methods: {
    async Dologout() {
      let ok = await JSON.parse(window.sessionStorage.getItem('user'))
      if (ok) {
        window.sessionStorage.removeItem('user')
        this.$router.push('/')
      }
      return this.$router.replace('/')
    },
  },
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
