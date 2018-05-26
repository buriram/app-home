<template>
  <v-parallax src="/pic/background.png" height="643">
    <v-flex xs12 sm6 offset-sm3>
      <v-card color="transparent">
        <v-card-media
          height="593px"
          contain
          src="/pic/logo.png"
        >  
        </v-card-media>
        <div class="text-xs-center">
          <v-btn color="orange">Continue to program</v-btn>
        </div>
      </v-card>
    </v-flex>
  </v-parallax>
</template>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
b {
  color: darkgoldenrod;
}
</style>