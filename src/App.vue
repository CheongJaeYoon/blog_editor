<template>
  <div id="app">
    <div id="side-menu">
      <SideMenu/>
    </div>
    <div id="editor">
      <Editor/>
    </div>
  </div>
</template>

<script>
import Editor from './components/Editor.vue'
import SideMenu from './components/SideMenu.vue'

export default {
  name: 'App',
  components: {
    Editor,
    SideMenu,
  }
}
</script>

<style>
html, head, body{
  height: 100%;
  widows: 100%;
  margin: 0;
}
#app {
  height: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: row;
}
#side-menu{
  width: 20%;
}
#editor{
  width: 80%;
}
</style>
