<template>
  <div>
    <h1>{{msg}}</h1>
    <button v-on:click="onClickMe">open mouse</button>
  </div>
</template>

<script>
export default {
  data: function(){
    return{
      msg:'hello from component a!'
    }
  },
  props:['msgfromfather'],
  methods:{
    onClickMe:function(){
      this.$emit('child-tell-me-something',this.msg);
    }
  }
}
</script>
<style>
</style>