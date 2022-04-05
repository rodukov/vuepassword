<template>
<div class="homepassword">

  <p>Password: <span style="color: green; text-decoration: underline; ">{{ this.password }}</span></p>
</div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return { 
      vueletters: "qwertyuiopasdfghjklzxcvbnm1234567890[]{}\|/:;',./<>?~`!@#$%^&*()_+-=",
      vuelength: 35,
      password: ""
    }
  },
  mounted() {
    var output = "";
    var len = this.vuelength;

    for(var i = 0; i < len; i++) {
      output += this.vueletters[this.vuepassword(this.vueletters.length)];
    }
    this.password = output;
  },
  methods: { // [Vue] Functions are stored there
    vuepassword(maximum) { return Math.floor( maximum * Math.random() ) } // [VuePassword] Generate new value
  }
}
</script>

<style scoped>
.homepassword {
  min-height: 1500px;
}
</style>