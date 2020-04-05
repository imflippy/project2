<template>
  <footer>
    <a href="https://www.linkedin.com/in/filip-minic-4963a0175/">Filip Minic 138/17</a>
    <a href="https://github.com/imflippy/project2">GitHub</a>
    <a href="documentation.pdf">Documentation</a>
</footer>
</template>

<script>
export default {
    name: 'Footer'
}
</script>

<style lang="scss" scoped>
    footer {
        display: flex;
        justify-content: space-around;
        align-items: center;
        border-top: 1px solid #797b80;
        height: 80px;
        a {
          color: #797b80;
          font-size: 16px;
        }
    }
</style>
