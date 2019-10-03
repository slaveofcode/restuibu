<template>
  <div>
    Directory
    <router-link :to="{ name: 'landing-page' }">Home</router-link>
    <router-link :to="{ name: 'request-page', params: { method: 'get' } }">Request Get</router-link>
  </div>
</template>