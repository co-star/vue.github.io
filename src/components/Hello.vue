<template>
  <div class="hello">
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
  name: 'hello',
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.finished{
  color: #999;
}
.hello {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.hello h1{
  width: 500px;
  min-height: 100px;
  margin: 0 auto;
  color: #fff;
  background-color: #365;
}
.hello div{
  width: 500px;
  min-height: 100px;
  margin: 0 auto;
  color: #000;
}
</style>
