<!-- <template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://gitter.im/vuejs/vue" target="_blank">Gitter Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
      <br>
      <li><a href="http://vuejs-templates.github.io/webpack/" target="_blank">Docs for This Template</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
  </div>
</template> -->

// <script>
// export default {
//   name: 'hello',
//   data () {
//     return {
//       msg: 'Welcome to Your Vue.js App'
//     }
//   }
// }
// </script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>

<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <input v-model="newItem" @keypress.enter="addNew()">
    <button @click="addNew()">{{buttonText}}</button>
    <ul v-if="items.length > 0">
      <h5>todo list</h5>
      <li v-for="(item,index) in items" v-bind:class="{finished: item.isFinished}" v-on:click="toggleFinish(item)">
        <button v-on:click.stop="item.quantity += 1" v-show="item.quantity < 5">
          +
        </button>
        {{item.quantity}}
        <button @click.stop="item.quantity -= 1" v-show="item.quantity > 1">
          -
        </button>
        {{item.label}}
        <button v-on:click="deleteItem(index)">
          x
        </button>
        <a href="" @click.prevent.stop>{{ love }}</a>
      </li>
    </ul>
    <ul>
      <li>Total Todos:{{ totalTodo }}<span>Updated:{{ totalTodosUpdated }}</span></li>
      <li>Total Todo Species:{{ totalTodoSpecie }}<span>Updated:{{ totalTodoSpeciesUpdated }}</span></li>
    </ul>
  </div>
</template>

<script>
import Store from './store'
export default {
  name: 'app',
  data: function(){
    return {
      title: 'this is a title !',
      love: 'Todo it !',
      totalTodosUpdated: 0,
      totalTodoSpeciesUpdated: 0,
      buttonText: "Add",
      items: Store.fetch(),
      newItem: ''
    }
  },
  methods:{
    toggleFinish: function(item){
      item.isFinished = !item.isFinished
    },
    addNew: function(){
      this.items.push({
        label: this.newItem,
        isFinished: false,
        quantity: 1
      });
      this.newItem = '';
    },
    deleteItem:function(index){
      this.items.splice(index,1);
    }
  },
  watch:{
    items:{
      handler:function(items){
        Store.save(items);
      },
      deep: true
    }
  },
  filter:{
    capitalize: function(value){
      if(!value)return'';
      value = value.toString();
      return value.charAt(0).toUpperCass()+value.slice(1);
    },
    undercass:function(value){
      if(!value)return'';
      value = value.toString();
      return value.tolomerCass();
    },
    url:function(value){
      if(!value)return'';
      value = value.toString();
      return "https://www.baidu.com"+value;
    }
  },
  computed:{
    totalTodo:function(){
      this.totalTodosUpdated += 1;
      var sum = 0;
      var items = this.items;
      for(var i in items){
        sum += items[i].quantity;
      }
      return sum;
    },
    totalTodoSpecie:function(){
      this.totalTodoSpeciesUpdated += 1;
      return this.items.length;
    }
  }
}
</script>

<style>
.finished{
  color: #999;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#app h1{
  width: 500px;
  min-height: 100px;
  margin: 0 auto;
  color: #fff;
  background-color: #365;
}
#app div{
  width: 500px;
  min-height: 100px;
  margin: 0 auto;
  color: #000;
}
</style>
