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
          <b-input v-model="result" type="textarea" />
        </b-field>
      </section>
      <section>
        <div class="buttons">
          <b-button type="is-primary"  rounded outlined @click="send()">Send</b-button>
        </div>
      </section>
      <router-link :to="{ name: 'landing-page' }">Home</router-link>
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
      result: undefined
    }
  },
  methods: {
    async send () {
      // const request = remote.net.request({
      //   method: this.method,
      //   url: this.url,
      //   redirect: 'follow'
      // })

      // request.setHeader('Accept', 'application/json')

      // if (this.method !== 'GET') {
      //   request.setHeader('Content-Type', 'application/json')
      //   request.write(JSON.stringify(this.params), 'utf-8')
      // }

      // request.on('finish', (res) => {
      //   console.log('finished')
      // })

      // request.on('response', (res) => {
      //   console.log('response', res)
      //   this.result = res.data
      // })

      // request.end()

      const res = await this.$http({
        method: this.method,
        url: this.url
      })

      console.log(res)

      this.result = JSON.stringify(res.data)
    }
  }
}
</script>