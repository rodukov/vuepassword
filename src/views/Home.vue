<template>
<div class="homepassword">

a
<div class="vuepassword-component">
  <div><input type="range" min=8 max=45 v-model="vuelength" @change="generate"><span>{{ vuelength }}</span></div>
  <div><input type="checkbox" v-model="include['numbers']" @change="generate"><span>Include numbers</span></div>
  <div><input type="checkbox" v-model="include['letters']" @change="generate"><span>Include letters</span></div>
  <div><input type="checkbox" v-model="include['symbols']" @change="generate"><span>Include symbols</span></div>
  <div><p style="text-align: center;"><button v-on:click="generate" class="button">Give me another password</button></p></div>
  <div><p>Password: <span style="color: green; text-decoration: underline; ">{{ this.password }}</span></p></div>
</div>

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
      include: { "numbers": true, "letters": true, "symbols": true },
      lastinclude: "", // add soon
      options: ["numbers", "letters", "symbols"]
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
      if(!this.include["numbers"] && !this.include["letters"] && !this.include["symbols"]) { this.include[this.options[this.vuepassword(3)]] = true; }
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

}
.vuepassword-component {
  /* Aligment */
  width: 500px;
  padding: 5%;
  margin-left: auto;
  margin-right: auto;
  margin: auto;
  /* Customization */
  background: white;
  border: 1px solid rgb(202, 202, 202);
  border-radius: 7px;

}
.button {
  padding: 3%;
  color: white;
  border: none;
  border-radius: 3px;
  font-family: 'Raleway', cursive;
  font-size: 15px;
  font-family: 'Karla', sans-serif;
  transition: 0.2s;
  /* background changing */
  background: linear-gradient(125deg, #3b9e1c, #1665c1, red);
  background-size: 400% 400%;
  animation: BackgroundGradient 5s ease infinite;
}
.button:hover { border-radius: 5px; transition: 0.01s;}
/* .button:active { background : #2ea543; box-shadow: 0px 0px 20px #2ea543;} */

@keyframes BackgroundGradient {
  0% {background-position: 0% 50%;}
  50% {background-position: 100% 50%;}
  100% {background-position: 0% 50%;}
}
</style>