<template>
<div class="homepassword">

<div class="vuepassword-component">
  <div><p style="text-align: center; margin: 0;"><img src="../assets/logo.png" style="width: 32px; height: 32px;"></p><p style="text-align: center; margin-top: 0%; font-family: Karla; font-size: 29px; margin-bottom: 8px; ">Vue Password</p></div>
  <p style="text-align: center; font-family: Karla; margin-top: 0;">{{ phraseToPage }}</p>

  <div class="config" style=" display: inline-block; margin: auto; ">
    <label class="container checkbox-text" >Include numbers<input class="checkbox" type="checkbox" v-model="include['numbers']" @change="generate"><span class="checkmark"></span></label>
    <label class="container checkbox-text">Include letters<input class="checkbox" type="checkbox" v-model="include['letters']" @change="generate"><span class="checkmark"></span></label>
    <label class="container checkbox-text">Include symbols<input class="checkbox" type="checkbox" v-model="include['symbols']" @change="generate"><span class="checkmark"></span></label>
    <!-- OLD Markup div><input class="checkbox" type="checkbox" v-model="include['numbers']" @change="generate"><span class="checkbox-text">Include numbers</span></div>
    <div><input class="checkbox" type="checkbox" v-model="include['letters']" @change="generate"><span class="checkbox-text">Include letters</span></div>
    <div><input class="checkbox" type="checkbox" v-model="include['symbols']" @change="generate"><span class="checkbox-text">Include symbols</span></div-->
    <div><input class="slider" type="range" min=8 max=45 v-model="vuelength" @change="generate"><span style="font-family: Karla; color: #535353;">{{ vuelength }}</span></div>
  </div>

  <div><p style="text-align: center;"><button v-on:click="generate" class="button">Give me another password</button></p></div>
  <div><p class="password-label" ><span v-show="false">Password: </span><span class="password-answer">{{ this.password }}</span></p></div>
</div>
</div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      passwordbasic: {"numbers": "1234567890", "letters": "qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM", "symbols": "[]{}\|/:;',./<>?~`!@#$%^&*()_+-="},
      vuelength: 25,
      password: "",
      include: { "numbers": true, "letters": true, "symbols": false },
      lastinclude: "", // add soon
      options: ["numbers", "letters", "symbols"],
      phrase: ["Include me on your site", "The easiest password generator in the world", "Written in Vue.js", "Open Source", "I recommend that you choose a longer password", "Also use symbols!", "The most important thing for your account is a good password", "Good utility to make your passwords secure!"],
      emo: ['😀', '😃', '😄', '🥲', '☺️', '😊', '😇', '🙂', '🙃', '😉', '😌', '😍', '🥰', '😘', '😗', '😙', '😚', '😋', '😛', '😝', '😜', '🤪', '🧐', '🤓', '😎', '🥸', '🤩', '🥳', '😏', '😈', '🙏', '🔓', '🔒', '🔐', '🔏', '📍', '📌', '🔗', '🧷', '🖇', '📎'],
      phraseToPage: ""
    }
  },
  mounted() {

    this.generate()
    this.select_phrase()
    // document.title = this.password
    
  },
  methods: {
    select_phrase() {
      this.phraseToPage = this.emo[this.vuepassword(this.emo.length)] + ' ' + this.phrase[this.vuepassword(this.phrase.length)];
    },
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
.homepassword { margin: 1%; }
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
  box-shadow: 0px 0px 100px rgb(228, 228, 228);

}
.button {
  padding: 3%;
  color: white;
  background: #40B782;
  border: none;
  border-radius: 3px;
  font-family: 'Raleway', cursive;
  font-size: 15px;
  font-family: 'Karla', sans-serif;
  transition: 0.25s;
}
.button:hover { border-radius: 8px; transition: 0.01s;
  /* background changing */
  background: linear-gradient(125deg, #40B782, rgb(77, 206, 152), rgb(114, 138, 216));
  background-size: 400% 400%;
  animation: BackgroundGradient 5s ease infinite;
}

@keyframes BackgroundGradient {
  0% {background-position: 0% 50%;}
  50% {background-position: 100% 50%;}
  100% {background-position: 0% 50%;}
}

.checkbox-text {
  font-family: Karla;
}


 /* Customize the label (the container) */
.container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 18px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.password-label {
  font-family: Karla;
  font-size: 19px;
  margin-top: 5%;
  text-align: center;
}

.password-answer {
  font-family: Karla;
  font-size: 19px;
  margin-top: 5%;
  text-decoration: underline;
  color: rgba(0, 196, 105, 0.767);
  border-radius: 10px;
  padding: 10px;
  transition: 0.3s;
}
.password-answer:hover {
  color: rgba(25, 126, 156, 0.658);
  background: rgba(12, 156, 84, 0.212);
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: rgb(240, 240, 240);
  border-radius: 4px;
  transition: 0.3s;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #40B782;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);

} 

/* The slider itself */
.slider {
  -webkit-appearance: none;  
  appearance: none;
  width: 100%;
  height: 15px;
  background: #e7e7e7; 
  outline: none; 
  opacity: 0.7;
  -webkit-transition: .2s; 
  transition: opacity .2s;
  border-radius: 4px;
}

/* Mouse-over effects */
.slider:hover {
  opacity: 1; 
}

/* The slider handle (use -webkit- (Chrome, Opera, Safari, Edge) and -moz- (Firefox) to override default look) */
.slider::-webkit-slider-thumb {
  width: 25px; 
  height: 25px;
  background: #40B782;
  cursor: pointer; 
  border: none;
}

.slider::-moz-range-thumb {
  width: 25px; 
  height: 25px;
  background: #40B782;
  cursor: pointer;
  border: none;
  animation: vuepassword 3s ease infinite;
}

@keyframes vuepassword {
  0% { box-shadow: 0px 0px 1px rgb(4, 170, 109); }
  100% { box-shadow: 0px 0px 50px rgb(4, 170, 109);  }
}
</style>