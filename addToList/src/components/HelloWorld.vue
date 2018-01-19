<template>
  <div class="hello">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew()"></input>
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click = "toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
    <p> child tells me: {{childwords}}</p>
    <componentA msgfromfather='you die!' v-on:child-tell-me-something='listenToMyBoy'></componentA>
  </div>
</template>

<script>
import Store from '../store'
import ComponentA from './componentA'
export default {
  name: 'HelloWorld',
  data () {
    return {
      title: 'this is a todo list',
      items:Store.fetch(),
      newItem:'',
      childwords:''
    }
  },
  components:{ComponentA},
  watch:{
    items:{
      handler:function(items){
        Store.save(items);
      },
      deep:true
    }
  },
  methods:{
    toggleFinish:function(item){
      item.isFinished = !item.isFinished;
    },
    addNew:function(){
      this.items.push({
          label:this.newItem,
          isFinished:false
      })
      this.newItem="";
    },
    listenToMyBoy:function(msg){
      this.childwords = msg;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
.finished{
  text-decoration:underline;
}
a {
  color: #42b983;
}
</style>
