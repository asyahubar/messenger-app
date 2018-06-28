<template>
  <div id="app">
    <SideList></SideList>
    <MessageWindow></MessageWindow>
  </div>
</template>

<script>
  import SideList from './components/SideList.vue'
  import MessageWindow from './components/MessageWindow.vue'

export default {
  name: 'app',
  components: {
      SideList,
      MessageWindow
  }
}
</script>

<style>
body {
    margin: 0;
    padding: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*width: 100vw;*/
  max-height: 100vh;
    display: flex;
}
</style>
