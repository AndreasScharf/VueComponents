<template>
  <div class="combobox">
    <div class="opener" v-on:click="combobox_open = true">
      <label class="text">{{ get_active_item() }}</label>
      <md-icon class="fa fa-bars"></md-icon>
    </div>
    <div class="background" :class="{'hide':!combobox_open}">
      <div class="box">
        <ul>
          <li v-for="(item, i) in items" :key="i + 'combobox_item'" v-on:click="item_selected(item) ">{{item.text}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'combobox',
  props: {items:Array},
  methods: {
    item_selected(item){
      this.items.forEach(e => e.active = false);
      item.active = true;

      this.combobox_open = false;
      this.$emit('item-select', item)
    }
  },
  data(){
    return{
      combobox_open: false,
      
      get_active_item(){return this.items.find(e => e.active).text}
    }
  }
}
</script>
<style>
.combobox .opener{

}
.combobox .background{
  background-color: var(--color7);
  
  position: fixed;
  top: 0;
  left: 0;

  width: 100%;
  height: 100%;
  z-index: 50;
  display: flex;
  flex-direction: column;
}
.combobox .background .box{
  flex: 0 0 auto;
  margin: 7.5%;
  background-color: var(--color1);
}
.combobox .background .box ul li{
  list-style: none;
}
.combobox .opener .text{
  margin-right: 10px;
}
</style>