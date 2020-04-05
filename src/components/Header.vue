<template>
  <header>
      <div class="logo">
          <img alt="Vue logo" src="../assets/logo.png" />
      </div>
      <div class="nav">
        <router-link to="/">Project2</router-link>
      </div>
  </header>
</template>

<script>
export default {
    name: 'Header'
}
</script>

<style lang="scss" scoped>
    header {
        display: flex;
        justify-content: space-around;
        height: 80px;
        border-bottom: 1px solid #797b80;
    }
    .nav {
        display: flex;
        align-items: center;
      a {
        color: #797b80;
        font-size: 30px;
        text-transform: uppercase;
      }
    }
    .logo {
        display: flex;
        align-items: center;
        img {
              height: 70%;
            }
    } 
</style>>
