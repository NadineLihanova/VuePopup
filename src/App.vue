<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="stylus">

body
  margin 0
  padding 0
  background url('./assets/images/bg.jpg') repeat
  overflow auto
  height auto
  font-family 'Roboto'
  &.stop-scroll
    overflow hidden
    height 100%

input 
    font-family 'Roboto'

</style>