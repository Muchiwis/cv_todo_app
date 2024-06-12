<template>
  <div id="app">
    <TodoApp />
  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue'
export default{
  name: 'App',
  components: {
    TodoApp
  }
}
</script>

<style>
/* Estilos para las clases title y content */
body{
  background: linear-gradient(135deg, #000000, #434343);
  height: 100vw;
}
#app {
  font-family: "Roboto", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}
.title {
  font-size: 40px;
  color: #FFF9D0;
  font-style: italic;
}
.sub-title{
  font-size: 18px;
  font-style: italic;
  color: #FFF9D0;
}
.nombre{
  font-size: 22px;
  color:#fff;
}
img {
    width: 100px;
    height: 100px;
  }
.headers{
  color: #FFF9D0;
    font-size: medium;
}
.text-buttom{
  font-family: "Roboto";
}
.estado{
  cursor: pointer;
}
</style>