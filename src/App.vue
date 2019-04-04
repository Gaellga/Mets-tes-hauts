<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/img/icon.png">
    <h1>Welcome to the weathsite</h1>
    <form>
      <div class="row">
        <div class="offset-md-3 col-md-6">
          <div class="form-group">
            <input type="text" class="form-control" aria-describedby="browsecity" placeholder="Enter city">
          </div>
        </div>
      </div>
      <div class="row">
        <div class="offset-md-2col-md-8">
          <div class="row">
            <div class="col-md-12">
              <HelloWorld/>
            </div>
          </div>
          <div class="row">

          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
