<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew" placeholder="add something"/>
    <ul>
      <li class="li"v-for="item in items" v-bind:class="{ finished:item.isFinished }" v-on:click="dothis(item)">
        {{item.label}}

      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store.js'
export default {
  data () {
    return {
      title: 'this is a todo list',
      items: Store.fetch(),
      newItem: ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }
  },
  methods: {
    dothis (item) {
      item.isFinished = !item.isFinished
    },
    addNew () {
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
li{
  list-style:none;
  padding:10px 0;
}
.finished {
  text-decoration: line-through;
  color:red;
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
