<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view></router-view>
    <h1>{{ title }}</h1>
    <input v-model="newItem" v-on:keyup.enter="addItem">
    <ul v-for="item in items">
      <li v-bind:class="{finished : item.isFinished}" v-on:click="toggleFun(item)">{{ item.label }}</li>
    </ul>
    <halou></halou>

  </div>

</template>

<script>
  import Store from './store'
  import Halou from './components/halou'

  console.log(Store)
  export default {
    name: 'app',
    data () {
      return {
        title: 'this is a todo list',
        items: Store.fetch(),
        newItem: ''
      }
    },
    components: {Halou},
    watch: {
      items: {
        handler: function (items) {
          Store.save(items)
        },
        deep: true
      }
    },
    methods: {
      toggleFun: function (item) {
        item.isFinished = !item.isFinished
      },
      addItem: function () {
        console.log(this.newItem)
        this.items.push({
          label: this.newItem,
          isFinished: false
        })
        this.newItem = ''
      }
    }
  }
</script>

<style>
  .finished {
    text-decoration: underline;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
