<template>
  <div class="home">
    <img alt="NyanCatto" src="../../public/images/Nyancatto.gif">
    <HelloWorld msg="LET'S RATE CATTOS!"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>
