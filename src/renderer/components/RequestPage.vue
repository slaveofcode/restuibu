<template>
  <div class="container">
    <div class="canvas">
      <section>
        {{ method }}
        <b-field>
          <b-input v-model="url" placeholder="URL address" type="text" />
        </b-field>
        <b-field>
          <b-input v-model="params" placeholder="Params" type="textarea" />
        </b-field>
      </section>
      <section>
        <b-field>
          <b-input v-model="resultData" placeholder="Result" type="textarea" />
        </b-field>
      </section>
      <section>
        <div class="buttons">
          <b-button type="is-primary"  rounded outlined @click="send()">Send</b-button>
        </div>
      </section>
      <router-link :to="{ name: 'directory-page' }">Home</router-link>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.canvas {
  padding: 1rem;
}
</style>

<script>
import { remote } from 'electron'

export default {
  created () {
    console.log(remote)
  },
  data () {
    return {
      method: this.$route.params.method.toUpperCase(),
      url: undefined,
      params: undefined,
      resultStatusCode: undefined,
      resultData: undefined,
      resultHeaders: undefined
    }
  },
  methods: {
    async send () {
      const res = await this.$http({
        method: this.method,
        url: this.url
      })

      console.log(res)
      this.resultHeaders = res.headers
      this.resultStatusCode = res.status
      this.resultData = JSON.stringify(res.data)
    }
  }
}
</script>