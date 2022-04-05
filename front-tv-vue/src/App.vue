<template>
  <div class="app-div">
    <Header />
    <Options />
    <Main />
    <Bus />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue';


export default {
  name: 'app',
  components: {
        Header,
        Main,
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family:'Comfortaa', cursive;
  

}
</style>
