<template>
  <div id="app">
    <Header />
    <div class='content'>
      <router-view />
    </div>

    <Footer/>
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
export default {
  components: {
    Header,
    Footer
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-color: #32363d;

}
.content {
  height: calc(100vh - 160px);
}
a {
  text-decoration: none;
}
</style>
