<template>
  <div>
    Request {{ method }}
    <router-link :to="{ name: 'landing-page' }">Home</router-link>
  </div>
</template>

<script>
export default {
  created () {
    console.log(this.$route)
  },
  data () {
    return {
      method: this.$route.params.method
    }
  }
}
</script>