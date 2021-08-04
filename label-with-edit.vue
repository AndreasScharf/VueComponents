<template>
  <div class="label-with-edit">
    <div :class="{'hide':item.edit}" v-on:click="go_edit()">{{item.name}}</div>
    <input type="text" :class="{'hide':!item.edit}" v-model="item.name" v-on:keyup.enter="leave_edit">
  </div>
</template>
<script>
export default {
  name: 'label-with-edit',
  props: {item:Object},
  methods:{
    go_edit(){
      this.$emit('deselect-all', 'lol');
      this.item.edit = true;
    },
    leave_edit(){
      this.item.edit = false
       this.$emit('leave-edit', 'lol');
    }
  },data(){

    return{
     
    }
  }
}
</script>
<style>
.label-with-edit{
  display: flex;
  flex-direction: column;
}
.label-with-edit div{
  cursor: pointer;
  text-align: center;
  font-size: var(--font1);

  margin: auto;

}
.label-with-edit input{
  margin: auto;

  font-size: var(--font1);

}
</style>