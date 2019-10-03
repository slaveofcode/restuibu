<template>
  <div>
    Directory
    <router-link :to="{ name: 'landing-page' }">Home</router-link>
    <router-link :to="{ name: 'request-page', params: { method: 'get' } }">Request GET</router-link>
    <router-link :to="{ name: 'request-page', params: { method: 'get' } }">Request POST</router-link>
    <router-link :to="{ name: 'request-page', params: { method: 'get' } }">Request PUT</router-link>
  </div>
</template>