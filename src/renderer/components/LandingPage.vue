<template>
  <div id="wrapper">
    <b-navbar>
      <template slot="start">
        <b-navbar-item href="#">
          Home
        </b-navbar-item>
        <b-navbar-item href="#">
          Documentation
        </b-navbar-item>
        <b-navbar-dropdown label="Info">
          <b-navbar-item href="#">
            About
          </b-navbar-item>
          <b-navbar-item href="#">
            Contact
          </b-navbar-item>
        </b-navbar-dropdown>
      </template>

      <template slot="end">
        <b-navbar-item tag="div">
          <div class="buttons">
            <a class="button is-primary">
              <strong>Sign up</strong>
            </a>
            <a class="button is-light">
              Log in
            </a>
          </div>
        </b-navbar-item>
      </template>
    </b-navbar>
    <router-link :to="{ name: 'directory-page' }">Directory</router-link>
  </div>
</template>

<script>
import SystemInformation from './LandingPage/SystemInformation'
import { remote } from 'electron'

const db = remote.getGlobal('db')

export default {
  name: 'landing-page',
  components: { SystemInformation },
  created () {
    const initDir = db.get('directories')
      .find({ name: 'default' })
      .value()
    if (!initDir) {
      db.get('directories')
        .push({ name: 'default', createdAt: new Date() })
        .write()
    }
    console.log(initDir)
  },
  methods: {
    open (link) {
      this.$electron.shell.openExternal(link)
    }
  }
}
</script>

<style>
#wrapper {
  background: #eeeeee;
  height: 100vh;
}
</style>
