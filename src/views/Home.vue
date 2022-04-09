<template>
  <div class="Home">
    <vuepassword/> <!-- Just add this to your vue website -->
  </div>
</template>

<script>
import vuepassword from '../components/vuepassword.vue'

export default {
  name: 'Home',
  components : { vuepassword }
}
</script>
