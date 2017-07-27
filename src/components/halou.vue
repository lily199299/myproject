<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{ msgFromfather }}</h2>
    <button v-on:click="onClickMe()">Click!</button>
  </div>
</template>

<script>
  export default {
    name: 'hello',
    data () {
      return {
        msg: 'Welcome to halou'
      }
    },
    props: ['msgFromfather'],
    methods: {
      onClickMe: function () {
        console.log(this.msgFromfather)
        this.$emit('tellsth', this.msg)
      }
    }

  }
</script>

<style scoped>
  h1, h2 {
    font-weight: normal;
  }
</style>
