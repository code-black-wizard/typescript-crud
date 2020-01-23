<template>
  <div id="app">
    <TheNavBar />
    <keep-alive>
      <router-view/>
    </keep-alive>
  </div>
</template>

<script>
// @ is an alias to /src
import TheNavBar from '@/components/UI/TheNavBar.vue'

export default {
  name: 'App',
  components: {
    TheNavBar
  }
}

</script>

<style>
@import '~bootstrap/dist/css/bootstrap.min.css';
@import '~@fortawesome/fontawesome-free/css/all.min.css';
</style>
