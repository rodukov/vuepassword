<template>
<div class="homepassword">

  <div><input type="range" min=8 max=45 v-model="vuelength"><span>{{ vuelength }}</span></div>
  <div><input type="checkbox" v-model="include['numbers']"><span>Include numbers</span></div>
  <div><input type="checkbox" v-model="include['letters']"><span>Include letters</span></div>
  <div><input type="checkbox" v-model="include['symbols']"><span>Include symbols</span></div>
  <button v-on:click="generate">Generate!</button>
  <p>Password: <span style="color: green; text-decoration: underline; ">{{ this.password }}</span></p>
</div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      passwordbasic: {"numbers": "1234567890", "letters": "qwertyuiopasdfghjklzxcvbnm", "symbols": "[]{}\|/:;',./<>?~`!@#$%^&*()_+-="},
      vuelength: 25,
      password: "",
      include: { "numbers": true, "letters": true, "symbols": true }
    }
  },
  mounted() {
    this.generate()
  },
  methods: {
    generate() { 
      var output = "";
      var len = this.vuelength;
      var buildbasic = "";
      if(this.include["numbers"]) { buildbasic += this.passwordbasic["numbers"] }
      if(this.include["letters"]) { buildbasic += this.passwordbasic["letters"] }
      if(this.include["symbols"]) { buildbasic += this.passwordbasic["symbols"] }

      for(var i = 0; i < len; i++) {
        var random = this.vuepassword(buildbasic.length);
        output += buildbasic[random];
      }
      this.password = output;
    },
    vuepassword(maximum) { return Math.floor( maximum * Math.random() ) } // [VuePassword] Generate new value
  }
}
</script>

<style scoped>
.homepassword {
  min-height: 1500px;
}
</style>